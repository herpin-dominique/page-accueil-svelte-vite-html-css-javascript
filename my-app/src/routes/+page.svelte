<script>
    import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	const [send, receive] = crossfade({
		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

	let todos = [
		{ id: 1, done: false, description: 'write some docs' },
		{ id: 2, done: false, description: 'start writing JSConf talk' },
		{ id: 3, done: true, description: 'buy some milk' },
		{ id: 4, done: false, description: 'mow the lawn' },
		{ id: 5, done: false, description: 'feed the turtle' },
		{ id: 6, done: false, description: 'fix some bugs' },
	];

	let uid = todos.length + 1;

	function add(input) {
		const todo = {
			id: uid++,
			done: false,
			description: input.value
		};

		todos = [todo, ...todos];
		input.value = '';
	}

	function remove(todo) {
		todos = todos.filter(t => t !== todo);
	}
        let color = '#FF5349';
        let name = 'tout le monde';
	    let upper = false;
        $: greeting = `Salut ${name}!`;
        $: casedGreeting = upper ? greeting.toUpperCase() : greeting;
	
        let src = "/src/photosmc.jpg";
	let name1 = 'smcaen';

</script>
<img {src} alt="{name1} soccer">
<h1 style="color: {color}">{casedGreeting}</h1>
<label><input type="checkbox" bind:checked={upper}> Uppercase </label>
<label for="name">Votre nom</label>
<input id="name" bind:value={name}>

<label for="color">Couleur </label>
<input id="color" type="color" bind:value={color}>

<div style="background-color: {color}" class="swatch" />
<h1 style="color: {color}">Salut {name}!</h1>



<h1>Hello {name}!</h1>


<h1>bienvenue chez moi</h1>
<p>ALLEZ MALHERBE !! <a href="https://www.smcaen.fr/">YOU CAN DO IT</a> Pour voir le site</p>
<div class='board'>
	<input
		class="new-todo"
		placeholder="Qu'est-ce que je dois faire?"
		on:keydown="{event => event.key === 'Enter' && add(event.target)}"
	>

	<div class='left'>
		<h2>A FAIRE</h2>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
				animate:flip
			>
				<input type=checkbox bind:checked={todo.done}>
				{todo.description}
				<button on:click="{() => remove(todo)}">x</button>
			</label>
		{/each}
	</div>

	<div class='right'>
		<h2>FAIT</h2>
		{#each todos.filter(t => t.done) as todo (todo.id)}
			<label
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
				animate:flip
			>
				<input type=checkbox bind:checked={todo.done}>
				{todo.description}
				<button on:click="{() => remove(todo)}">x</button>
			</label>
		{/each}
	</div>
</div>

<style>
    .swatch {
        display: inline-block;
        height: 20px;
        width: 20px;
    }
    .new-todo {
		font-size: 1.4em;
		width: 100%;
		margin: 2em 0 1em 0;
	}

	.board {
		max-width: 36em;
		margin: 0 auto;
	}

	.left, .right {
		float: left;
		width: 50%;
		padding: 0 1em 0 0;
		box-sizing: border-box;
	}

	h2 {
		font-size: 2em;
		font-weight: 200;
		user-select: none;
	}

	label {
		top: 0;
		left: 0;
		display: block;
		font-size: 1em;
		line-height: 1;
		padding: 0.5em;
		margin: 0 auto 0.5em auto;
		border-radius: 2px;
		background-color: #eee;
		user-select: none;
	}

	input { margin: 0 }

	.right label {
		background-color: rgb(180,240,100);
	}

	button {
		float: right;
		height: 1em;
		box-sizing: border-box;
		padding: 0 0.5em;
		line-height: 1;
		background-color: transparent;
		border: none;
		color: rgb(170,30,30);
		opacity: 0;
		transition: opacity 0.2s;
	}

	label:hover button {
		opacity: 1;
	}
    

</style>