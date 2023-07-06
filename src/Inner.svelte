<script>

import { createEventDispatcher } from 'svelte';

const dispatch = createEventDispatcher();

function sayHello() {
    dispatchEvent('message', {
        text: 'Hello!'
    });
}
// `createEventDispatcher` must be called when the component is first instantiated - you can't do it later inside e.g. a `setTimeout` callback. This links `dispatch` to the component instance.

// You can also try changing the event name to something else. For instance, change `dispatch('message', {...})` to `dispatch('gree',{...})` in Inner.svelte and change the attribute name from `on:message` to `on:greet` in App.svelte.
</script>

<button on:click={sayHello}>
    Click to say Hello
</button>

