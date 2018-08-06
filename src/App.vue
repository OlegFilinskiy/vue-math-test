<template>
  <div class="training">
      <h1>Math training</h1>
      <hr>
      <startScreen v-if="state == 'start'"
        @onStart="onStart" 
      ></startScreen> <!-- @onStart подписывает на кастомное событие, сгенерированное в template с ппомощью $emit -->
      <question v-else-if="state == 'question'"></question>
      <message v-else-if="state == 'massege'"></message>
      <resultScreen v-else-if="state == 'results'"></resultScreen>
      <div v-else="state == 'start'">Unknown state</div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state: 'start'
    }
  },
  methods: {
    onStart() {
      this.state = 'question'
    }
  }
}
</script>

<style scoped>
  .training {
    max-width: 768px;
    margin: 0 auto;
  }
</style>
