<script>
	import { percentStore } from './store.js';
	export let flag;
	export let rightAnswer;
	export let answerArray;
	export let selectedAnswer;
	export let isButtonDisabled;

	let score = 0;
	let totalQuestions = 0;
	let percent;
	let buttonText = 'SUBMIT';
	isButtonDisabled = false;

	$: {
		if (!isButtonDisabled) {
			buttonText = 'SUBMIT';
		}
	}
	function handleRadioSubmit(event) {
		selectedAnswer = event.target.value;
	}

	function checkForAnswer() {
		if (selectedAnswer === rightAnswer) {
			buttonText = 'Correct!';
			score++;
		} else {
			buttonText = `Wrong! The answer: ${rightAnswer}`;
		}
		totalQuestions++;
		percent = totalQuestions > 0 ? (score / totalQuestions) * 100 : 0;
		percentStore.set(percent);
		console.log(score, totalQuestions, selectedAnswer, rightAnswer, percent);
		isButtonDisabled = true;
	}
</script>

<main>
	<div class="game-cont">
		<div id="image-cont">
			<img src={flag} alt={rightAnswer} />
		</div>

		<div class="options-cont">
			{#each answerArray as answer}
				<label
					><input
						type="radio"
						bind:group={selectedAnswer}
						value={answer}
						class="radio"
						on:submit={handleRadioSubmit}
					/>{answer}</label
				><br />
			{/each}
		</div>
	</div>
</main>

<div class="submit-btn-cont">
	<button on:click={checkForAnswer} disabled={isButtonDisabled}>{buttonText}</button>
</div>

<style>
	main {
		display: flex;
		flex-direction: column;
		width: 80%;
		margin: 10px;
		z-index: 2;
		position: relative;
	}
	.game-cont {
		background-color: var(--primary);
		border-radius: 6px;
		padding: 10px;
		display: flex;
		flex-direction: column;
		color: black;
		height: 350px;
		margin-top: -30px;
	}

	img {
		max-height: 200px;
		min-width: 340px;
		min-height: 150px;
	}
	.options-cont {
		margin-top: 20px;
		margin-bottom: -10px;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		margin-left: 50px;
	}
	label {
		margin: -10px;
		font-size: 22px;
	}
	.submit-btn-cont {
		width: 85%;
		margin: auto;
	}
	button {
		width: 90%;
		font-weight: 700;
		height: 90px;
		z-index: 3;
		margin: 10px auto 25px auto;
	}
</style>
