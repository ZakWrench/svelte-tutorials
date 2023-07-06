<!--first component-->
<script>
	let name = 'Svelte';
	let img_src = '/image.gif';
	let dance = "A man dances.";
	import Nested from './Nested.svelte';
	let parag1 = "This string contains some <strong>HTML!</strong>";
	
	let count = 0;
	function increment() {
		count += 1;
	}
	$: doubled = count * 2
	/*Reactive Statements*/
	$: {
		console.log('the count is ${count}');
		console.log('this will also be logged');
		if (count >= 10){
			alert('Count is dangerously high, resetting..');
			count = 0;
		}
	}
	let numbers = [1,2,3,4];
	function addNumber() {
		numbers = [...numbers, number.length + 1];
	}
	$: sum = numbers.reduce((total, currentNumber) => total + currentNumber, 0)

	import PackageInfo from './PackageInfo.svelte';
	const pkg = {
		name: 'svelte',
		speed: 'blazing',
		version: 4,
		website: 'https://svelte.dev'
	};

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
<!--Assignment-->
<button on:click={increment}>
	clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
<!--Reactive Declarations-->
<p>{count} doubled is {doubled}</p>
<!--Updating Arrays and Objects-->
<p>{numbers.join(' + ')} = {sum}</p>
<button on:click = {addNumber}>
	Click to add incremental numbers
</button>

<!--PROPS-->

<!--Declaring Props-->
<Nested answer = {43-1}/>

<!--Default Values-->
<Nested />

<!--Spread Props-->
<PackageInfo
	name = {pkg.name}
	speed= {pkg.speed}
	version = {pkg.version}
	website = {pkg.website}
/>