<template>
  <div class="training">
	  <h1>Math training. Level {{level + 1}}</h1>
	  <hr>
	  <div class="progress">
		<div class="progress-bar" :style="progressStyles"></div>
	  </div>
	  <div class="box">
	  	<transition name="flip" mode="out-in">
		  <startScreen v-if="state == 'start'"
					   @onStart="onStart" 
		  ></startScreen> <!-- @onStart подписывает на кастомное событие, сгенерированное в template с ппомощью $emit -->
		  <question v-else-if="state == 'question'"
					@success="onQuestSuccess"
					@error="onQuestError"
					:settings="levels[level]" 
		  ></question> <!-- :settings (v-bind:settings) передает props внутрь компонента -->
		  <message v-else-if="state == 'message'"
		  		   :type="message.type"
		  		   :text="message.text"
		  		   @onContinue="onContinue"
		  ></message>
		  <resultScreen v-else-if="state == 'results'"
		  				:stats="stats"
		  				@repeat="onStart"
		  				@nextLevel="nextLevel"
		  ></resultScreen>
		  <div v-else="state == 'start'">Unknown state</div>
	  	</transition>
	  </div>
  </div>
</template>

<script>
  export default {
	data () {
	  return {
		state: 'start',
		message: {
			type: '',
			text: ''
		},
		stats: {
			success: 0,
			error: 0
		},
		questMax: 3,
		level: 0,
		levels: [
			{
				from: 10,
				to: 40,
				range: 5,
				variants: 2
			},
			{
				from: 100,
				to: 200,
				range: 20,
				variants: 4
			},
			{
				from: 500,
				to: 900,
				range: 40,
				variants: 5
			}
		]
	  }
	},
	computed: {
		questDone() {
			return this.stats.success + this.stats.error;
		},
		progressStyles() {
			return {
				width: (this.questDone / this.questMax * 100) + '%'
			}
		}
	},
	methods: {
	  onStart() {
		this.state = 'question';
		this.stats.success = 0;
		this.stats.error = 0;
	  },
	  onQuestSuccess() {
		this.state = 'message';
		this.message.text = 'Good Job!';
		this.message.type = 'success';
		this.stats.success++;
	  },
	  onQuestError(msg) {
		this.state = 'message';
		this.message.text = msg;
		this.message.type = 'warning';
		this.stats.error++;
	  },
	  onContinue() {
	  	if(this.questDone < this.questMax) {
	  		this.state = 'question';
	  	} else {
	  		this.state = 'results';
	  	}
	  },
	  nextLevel() {
	  	this.level++;
	  	this.onStart();
	  }
	}
  }
</script>

<style scoped>
  .training {
	max-width: 768px;
	margin: 0 auto;
  }

  .box {
  	margin: 10px 0;
  }

  .flip-enter {

  }
  .flip-enter-active {
  	animation: flipInX .3s linear; 
  }
  .flip-leave {
  	
  }
  .flip-leave-active {
  	animation: flipOutX .3s linear; 
  }

  @keyframes flipInX {
  	from {transform: rotateX(90deg)}
  	to {transform: rotateX(0deg)}
  }

  @keyframes flipOutX {
  	from {transform: rotateX(0deg)}
  	to {transform: rotateX(90deg)}
  }
</style>
