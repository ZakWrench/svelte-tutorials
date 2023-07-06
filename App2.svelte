<script>
    let count = 0;

    function increment() {
        count += 1;
    }

    const colors = ['red',  'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
    let selected = colors[0];

    import Thing from './Thing.svelte';

    let things = [
        {id : 1, name: 'apple'},
        { id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' }
    ];

    function handleClick() {
        things = things.slice(1);
    }
</script>

<!--LOGIC-->

<!--if Logic-->
<button on:click ={increment}>
    Clicked {count}
    {count === 1 ? 'time' : 'times'}
</button>
{#if count > 10}
    <p>{count} is greater than 10</p>
<!--else if-->
{:else if count < 5}
    <p>{count} is less than 5</p>
<!--else-->
{:else}
    <p>{count} is between 5 and 10</p>
{/if}
<!--A `#` character always indicates a block opening tag. a `/` character always indicates a block closing tag. a `:` character
indicates a block continuation tag-->

<!--Each blocks-->
<h1 style="color: {selected}">Pick a colour</h1>

<div>
    {#each colors as color, i}
    <button
        aria-current={selected === color}
        aria-label={color}
        style="background: {color}"
        on:click={() => selected = color}
        >{i + 1}</button>
    {/each}
</div>


<style>
	h1 {
		transition: color 0.2s;
	}

	div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	}

	button {
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
	}

	button[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0,0,0,0.2);
	}
</style>

<!--Keyed each Blocks-->
<button on:click={handleClick}>
    Remove first Thing
</button>

{#each things as thing (thing.id)}
    <Thing name={thing.name} />
{/each}
<!-- We can use any object as the key, as Svelte uses a `Map` internally, in toher words we could do (thing) instead of (thing.id).
Using a string  or number is generally safer, however, since it means identity persists without referential equality, for example when updating with fresh data from an API server-->
