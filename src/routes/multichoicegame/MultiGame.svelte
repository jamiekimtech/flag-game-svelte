<script>
	export let flag;
	export let rightAnswer;
	export let answerArray;

	let selectedAnswer = '';
	let buttonText = 'SUBMIT';

	$: {
		if (rightAnswer) {
			selectedAnswer = '';
			buttonText = 'SUBMIT';
		}
	}

	function checkForAnswer() {
		if (selectedAnswer === rightAnswer) {
			buttonText = 'Correct!';
		} else {
			buttonText = `Wrong! The answer: ${rightAnswer}`;
		}
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
					/>{answer}</label
				><br />
			{/each}
		</div>
	</div>
</main>

<div class="submit-btn-cont">
	<button on:click={checkForAnswer}>{buttonText}</button>
</div>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
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
		min-width: 360px;
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
		width: 100%;
		font-weight: 700;
		height: 90px;
		z-index: 3;
		position: relative;
	}
</style>
