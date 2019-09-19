<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayHello() {
		dispatch('message', {
			increment: 1
		});
	}
</script>

<button on:click={sayHello}>
	Click to say hello
</button>