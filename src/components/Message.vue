<template>
    <div class="alert" :class="'alert-' + type">
    	<h3>{{ text }}</h3>
    	<hr>
    	<button class="btn btn-primary"
    			@click="$emit('onContinue')"
    	>
    		Continue
    	</button>
    </div>
</template>

<script>
    export default {
    	props: ['type', 'text']
    }
</script>

<style scoped>
	.alert {
		text-align: center;
	}
	.h3, .btn {
		margin: 30px 0;
		text-align: center;
	}
</style>