<script>
    let count = 0;

    function increment() {
        count += 1;
    }

    const colors = ['red',  'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
    let selected = colors[0];

    import Thing from './Thing.svelte';
  import PackageInfo from './src/PackageInfo.svelte';

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

    import { getRandomNumber } from './utils.js';

    let promise = getRandomNumber();

    function handleClick2(){
        promise = getRandomNumber();
    }

    let m = { x: 0, y: 0};

    function handleMove(event) {
        m.x = event.clientX;
        m.y = event.clientY;
    }

    import Inner from './Inner.svelte'

    function handleMessage(event) {
        alert(event.detail.text);
    }

    import BigRedButton from './BigRedButton.svelte';
    import horn from './horn.mp3';

    const audio = new Audio();
    audio.src = horn;

    function handleBRBClick() {
        audio.play();
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

<!--Await blocks-->
<button on:click={handleClick}>
    generate random number
</button>
{#await promise}
    <p>... waiting</p>
{:then number}
    <p>The number is {number}</p>
{:catch error}
    <p style = "color: red">{error.message}</p>
{/await}
<!--Only the most recent `promise` is considered, meaning you don't need to worry about race conditions.
On another note, if you know that your promise can't reject, you can omit the `catch` block. You can also omit the first block if 
you don't want to show anything until the promise resolves
{#await promise then number}<p>The number is {number}</p> {/await}-->

<!--EVENTS-->

<!--DOM Events-->
<div on:pointermove={handleMove}>
    The pointer is at {m.x} x {m.y}
</div>

<style>
    div {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100;
        padding: 1rem;
    }
</style>

<!--Inline Handlers-->
<div
    on:pointermove={(e) => {
        m = {x: e.clientX, y: e.clientY};
    }}
> The mouse position using inline handlers is {m.x} x {m.y}
</div>
<!-- In some frameworks you may see recommendations to avoid inline event handlers for performance reasons, particularly inside loops.
That advice doesn't apply to Svelte - the compiler will always do the right thing, whichever form you choose.-->

<!--Event Modifiers-->
<button on:click|capture|stopPropagation={() => alert('clicked')}>
    Click me
</button>

<!--Component Events-->
<Inner on:message={handleMessage} />

<!--DOM Event Forwarding-->
<BigRedButton on:click={handleBRBClick} />



