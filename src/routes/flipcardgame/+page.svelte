<script>
	import axios from 'axios';
	import Flashcard from './Flashcard.svelte';
	import GoHome from '../GoHome.svelte';

	let flag;
	let countryName;
	let promise = getRandomFlag();

	$: flag = promise.flag;
	$: countryName = promise.countryName;

	async function getRandomFlag() {
		try {
			const response = await axios.get('https://restcountries.com/v3.1/region/asia');
			const countries = response.data;

			// Select a random country from the response data
			const randomIndex = Math.floor(Math.random() * countries.length);
			const randomCountry = countries[randomIndex];

			// Assign the flag and country name from the random country
			flag = randomCountry.flags.png;
			countryName = randomCountry.name.common;
			answerVisible = false;
			console.log('WORKING!');
			return { flag, countryName };
		} catch (error) {
			console.error('ERROR!');
		}
	}

	function newGame() {
		promise = getRandomFlag();
	}

	let answerVisible = false;
	const toggleShowBack = () => (answerVisible = !answerVisible);
</script>

<main>
	<h1>Flip the Card to Reveal Answer</h1>
	<!-- FLASHCARD -->

	{#await promise}
		<p>...waiting</p>
	{:then promise}
		<div class="flip-box">
			<button
				on:click={toggleShowBack}
				class="flip-box-inner flip-btn"
				class:flip-it={answerVisible}
			>
				<Flashcard {flag} {countryName} {answerVisible} />
			</button>
		</div>
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}

	<!-- BUTTONS -->
	<div id="btn-cont">
		<button class="start-btn" on:click={newGame}>New Game</button>
	</div>
	<GoHome />
</main>

<style>
	h1 {
		margin-bottom: 20px;
	}
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 0px;
		height: 400px;
	}

	.flip-box {
		background-color: transparent;
		width: 400px;
		height: 500px;
		perspective: 1000px;
		border-radius: 1000px;
		display: flex;
		align-items: center; /* centers items vertically */
		justify-content: center;
		border-radius: 30px;
		border: none;
	}

	/* This container is needed to position the front and back side */
	.flip-box-inner {
		position: relative;
		width: 100%;
		height: 100%;
		text-align: center;
		transition: transform 0.8s;
		transform-style: preserve-3d;
		box-sizing: border-box;
		border-radius: 30px;
		border: none;
	}

	.flip-btn {
		background-color: var(--primary);
		max-width: 90%;
	}
	.flip-btn:hover {
		background-color: var(--primary);
	}

	/* Do an horizontal flip on button click */
	.flip-it {
		transform: rotateY(180deg);
	}

	#btn-cont {
		width: 200px;
		padding: 10px 0;
		display: flex;
		justify-content: space-between;
		margin-bottom: -20px;
	}

	button {
		color: black;
		font-weight: 600;
	}
</style>
