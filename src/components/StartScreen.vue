<template>
    <div class="alert alert-primary" role="alert">
    	<h3>Are you ready?</h3>
    	<hr>
    	<button class="btn btn-success" @click="$emit('onStart')">Start</button> <!-- $emit генерирует кастомное событие и передает родителю -->
    </div>
</template>

<script>
    export default {

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