<script>
	import Nested from './Nested.svelte'
	import Info from './Info.svelte'
	import Outer from './Outer.svelte';

	let name = 'svelte';
	let string = `this string contains some <strong>HTML!!!</strong>`;
	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};
	let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];

	let count = 0;
	$:doubled = count * 2;

	function handleClick() {
		count += 1;
	}

	$:if (count >= 10) {
		console.log(`the count is ${count}`);
	} 

	let numbers = [1, 2, 3, 4];

	function addNumbers(){
		numbers.push(numbers.length + 1)
		numbers = numbers;
	}

	$: sum = numbers.reduce((t, n) => t + n, 0)
	
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

	function handleMessage(event) {
		console.log(event.detail.count);
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name.toUpperCase()}!</h1>

<Nested answer={count}/>

<!-- <Info name={pkg.name} version={pkg.version} speed={pkg.speed} website={pkg.website}/> -->
<Info {...pkg}/>

<p>{@html string}</p>

<button on:click={handleClick}>Clicked {count}</button>

<p>clicked doubled {doubled}</p>

<button on:click|once={addNumbers}>Add number</button>

<p>{numbers.join('+')} = {sum}</p>

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

{#each cats as cat, i}
<p>{i + 1}) {cat.id}: {cat.name}</p>
{/each}

<Outer on:count={handleMessage}/>
