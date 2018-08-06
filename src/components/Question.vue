<template>
    <div class="alert alert-secondary">
    	<h3> {{x}} + {{y}} = ? </h3>
    	<hr>
    	<div class="buttons">
    		<button class="btn btn-success" v-for="number in answers">
    			{{number}}
    		</button>
    	</div>
    </div>
</template>

<script>
    export default {
    	data() {
    		return {
    			x: mtRand(100, 200),
    			y: mtRand(100, 200)
    		}
    	},
    	computed: {
    		answers() {
    			var good = this.x + this.y,
    				res = [good];

    			while (res.length < 4) {
    				var num = mtRand(good - 20, good + 20);

                    // если не содержит такое число, то добавляем в массив
    				if (res.indexOf(num) === -1) { 
    					res.push(num);
    				}
    			}

    			return res.sort(function() {
    				return Math.random() > 0.5;
    			});
    		}
    	}
    }

    function mtRand(min, max) {
    	let diff = max - min;

    	return Math.floor(Math.random() * (diff + 1)) + min;
    }
</script>

<style scoped>
	.alert {
		padding-top: 20px;
	}
	.buttons {
		display: flex;
		justify-content: space-around;
	}
</style>