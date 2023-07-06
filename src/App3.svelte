<script>
    let name = 'world';

    let a = 1;
    let b = 2;

    let yes = false;

    let questions = [
        {
            id: 1,
            text: 'Where did you go to school?'
        },
        {
            id: 2,
            text: "What is your mother's name?"
        }
    ];

    let selected;
    let answer = '';
    
    function handleSubmit() {
        alert(
            'answered question ${selected.id} (${selected.text}) with "${answer}"'
        );
    }
</script>

<!--BINDINGS-->

<!--Text Inputs-->
<input bind:value={name} />
<h1>Hello {name}!</h1>

<!--Numeric Inputs
In the DOM, everything is a string. Unhelpful when we're dealing with numeric inputs `type = "number" and type = "range", as it means we have to remember to coerce `input.value` before using it.-->
<label>
    <input type = "number" bind:value={a} min = "0" max = "10" />
    <input type = "range" bind:value={a} min= "0" max = "10" />
</label>

<label>
	<input type="number" bind:value={b} min="0" max="10" />
	<input type="range" bind:value={b} min="0" max="10" />
</label>

<p> {a} + {b} = { a + b }</p>

<!--Checkbox inputs-->
<label>
    <input type = "checkbox" bind:checked={yes} />
    Yes ! send me regular email spam
</label>

{#if yes}
    <p>
        Thank you. We will bombard your inbox and sell your personal data
    </p>
{:else}
    <p>
        You must opt in to continue. If you're not paying, you're the product.
    </p>
{/if}

<button disabled={!yes}>Subscribe</button>

<!--Select Bindings-->
<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
    <select
    value = {selected}
    on:change={() => (answer = '')}
    >
        {#each questions as question}
            <option value = {question}>
                {question.text}
            </option>
        {/each}
    </select>

    <input bind:value = {answer} />
    <button disabled = {!answer} type="submit">
        Submit    
    </button>
</form>

<p>
    selected question {selected
    ? selected.id
    : '[waiting...]'}
</p>
<!--Note that the <option> values are object rather than strings. Svelte doesn't mind.
Note: Because we haven't set an initial value of `selected`, the binding will set it to the default value(the first in the list) automatically.
Be careful though - until the binding is initialised, `selected` remains undefined, so we can't blindly reference e.getComputedStyle. `selected.id` in the template.   -->

<!--Group Inputs-->

