<script>
	import axios from 'axios';
	import GoHome from '../GoHome.svelte';
	import MultiGame from './MultiGame.svelte';
	import Score from './Score.svelte';

	let flag;
	let rightAnswer;
	let promise = getRandomQuiz();
	let answerArray = [];

	$: flag = promise.flag;
	$: rightAnswer = promise.rightAnswer;
	$: answerArray;

	async function getRandomQuiz() {
		try {
			const response = await axios.get('https://restcountries.com/v3.1/region/asia');
			const countries = response.data;

			// Select a random country from the response data
			const randomIndex = Math.floor(Math.random() * (countries.length - 2)) + 1;
			const randomCountry = countries[randomIndex];
			const wrongCountries = [
				countries[randomIndex - 1].name.common,
				countries[randomIndex + 1].name.common
			];

			// Assign the flag and country name from the random country
			flag = randomCountry.flags.png;
			rightAnswer = randomCountry.name.common;
			answerArray = [rightAnswer, ...wrongCountries].sort(() => 0.5 - Math.random());
			answerVisible = false;
			console.log('WORKING!');
			console.log(flag, rightAnswer, answerArray);
			return { flag, rightAnswer, answerArray };
		} catch (error) {
			console.error('ERROR!');
		}
	}

	function newGame() {
		promise = getRandomQuiz();
	}

	let answerVisible = false;
	const toggleShowBack = () => (answerVisible = !answerVisible);

	const viewScore = () => {
		showScore = true;
	};
</script>

<main>
	<h1>Choose One Answer</h1>
	{#await promise}
		<p>...waiting</p>
	{:then promise}
		<div class="game-box">
			<MultiGame {flag} {answerArray} {answerVisible} />
		</div>
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}

	<div id="btn-cont">
		<button on:click={newGame}>New Game</button>
		<button on:click={viewScore}>Your Score</button>
	</div>

	<GoHome />
</main>

<style>
	.game-box {
		max-width: 500px;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: auto;
	}
	#btn-cont {
		display: flex;
		justify-content: center;
		gap: 20px;
	}
	button {
		max-width: 170px;
		color: black;
		font-weight: 600;
		margin-bottom: 10px;
	}
</style>
