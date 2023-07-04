<script>
	export let flag;
	export let rightAnswer;
	export let answerArray;

	let selectedAnswer = '';
	let buttonText = 'Submit';
	let isButtonDisabled = false;

	function checkForAnswer() {
		isButtonDisabled = true;
		if (selectedAnswer === rightAnswer) {
			buttonText = 'Correct answer!';
		} else {
			buttonText = `Wrong answer! The correct answer was: ${rightAnswer}`;
		}
	}
</script>

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
				/>{answer}</label
			>
			<br />
		{/each}
	</div>
</div>

<div class="submit-btn-cont">
	<button on:click={checkForAnswer} disabled={isButtonDisabled}>{buttonText}</button>
</div>

<style>
	.game-cont {
		background-color: var(--primary);
		margin: auto;
		margin-bottom: 15px;
		margin-top: -40px;
		max-width: 450px;
		border-radius: 6px;
		padding: 10px;
		display: flex;
		flex-direction: column;
		color: black;
	}

	#image-cont {
		width: 450px;
	}
	.options-cont {
		margin-top: 20px;
		margin-bottom: -10px;
	}
	label {
		margin: -10px;
		font-size: 22px;
	}
	.submit-btn-cont {
		max-width: 450px;
	}
	button {
		width: 450px;
	}
</style>
