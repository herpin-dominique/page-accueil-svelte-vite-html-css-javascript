<script>
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
<style>
    .swatch {
        display: inline-block;
        height: 20px;
        width: 20px;
    }
</style>