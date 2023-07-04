<!--first component-->
<script>
	let name = 'Svelte';
	let img_src = '/image.gif';
	let dance = "A man dances.";
	import Nested from './Nested.svelte';
	let parag1 = "This string contains some <strong>HTML!</strong>";
</script>

<h1>Hello {name.toUpperCase()}</h1>
<!--Dynamic attributes-->
<img {img_src} alt= dance />
<!--Styling-->
<p> This is a paragraph.</p>
<style>
	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
<!--Nested Components-->
<!--styles applied to App.svelte don't leak to Nested.svelte-->
<Nested/>
<!--HTML tags rendering-->
<!--Warning: Svelte doesn't perform any sanitization of the expression inside{@html ...} before it gets inserted into the DOM. if it's some untrusted user content, e.g. a comment on an article, then it's critical that we manually escape it, otherwise we risk exposing our users to XSS attacks-->
<p>{@html parag1}</p>
<!--Reactivity-->