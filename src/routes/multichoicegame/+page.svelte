<script>
	import axios from 'axios';
	import GoHome from '../GoHome.svelte';
	import MultiGame from './MultiGame.svelte';
	import Score from './Score.svelte';
	import { spring, tweened } from 'svelte/motion';

	let flag;
	let rightAnswer;
	let selectedAnswer;
	let answerArray = [];
	let promise = getRandomQuiz();
	let showScore = false;
	let error = '';
	let score = 0;
	let totalQuestions = 0;

	let percent = 0;
	const store = tweened(0, { duration: 1000 });

	$: {
		percent = totalQuestions > 0 ? (score / totalQuestions) * 100 : 0;
		store.set(percent);
	}

	$: if (promise) {
		promise
			.then((result) => {
				flag = result.flag;
				rightAnswer = result.rightAnswer;
				answerArray = result.answerArray;
			})
			.catch((err) => {
				error = err.message;
			});
	}

	async function getRandomQuiz() {
		try {
			const response = await axios.get('https://restcountries.com/v3.1/region/asia');
			const countries = response.data;

			// Select a random country & 2 wrong countries from the response
			const randomIndex = Math.floor(Math.random() * (countries.length - 2)) + 1;
			const randomCountry = countries[randomIndex];
			const wrongCountries = [
				countries[randomIndex - 1].name.common,
				countries[randomIndex + 1].name.common
			];

			// Assign the flag and country names
			console.log('WORKING!', promise, score, totalQuestions);
			return {
				flag: randomCountry.flags.png,
				rightAnswer: randomCountry.name.common,
				answerArray: [randomCountry.name.common, ...wrongCountries].sort(() => 0.5 - Math.random())
			};
		} catch (error) {
			console.error('ERROR!');
		}
	}
	function checkAnswer(selectedAnswer) {
		totalQuestions++;
		if (selectedAnswer === rightAnswer) {
			score++;
		}
	}

	function newGame() {
		error = '';
		checkAnswer(selectedAnswer);
		promise = getRandomQuiz();
	}
	const viewScore = () => {
		showScore = !showScore;
	};
</script>

<main>
	<h1>Choose One Answer</h1>
	{#if error}
		<p style="color: red">{error}</p>
	{:else}
		<div class="game-box">
			{#if showScore}
				<Score {percent} />
				<MultiGame {flag} {rightAnswer} {selectedAnswer} {answerArray} />
			{:else}
				<MultiGame {flag} {rightAnswer} {selectedAnswer} {answerArray} />
			{/if}
		</div>
	{/if}
	<div id="btn-cont">
		<button on:click={newGame}>New Game</button>
		<button on:click={viewScore}>Your Score</button>
	</div>
	<GoHome />
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
		height: 600px;
	}
	.game-box {
		display: flex;
		flex-direction: column;
		align-items: center;
		min-width: 500px;
	}
	#btn-cont {
		display: flex;
		justify-content: center;
		gap: 30px;
		width: 60%;
	}
	button {
		color: black;
		font-weight: 600;
		margin-bottom: 10px;
		z-index: 1;
	}
</style>
