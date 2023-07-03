<script>
	import { countryData } from './countryData.js';
	import Flashcard from './Flashcard.svelte';

	let flashcardIndex = 0;
	$: clue = countryData[flashcardIndex].flag;
	$: answer = countryData[flashcardIndex].country;

	let showCardBack = false;
	const toggleShowBack = () => (showCardBack = !showCardBack);

	const prevCard = () => {
		showCardBack = false;
		if (flashcardIndex === 0) {
			flashcardIndex = countryData.length - 1;
		} else {
			flashcardIndex -= 1;
		}
	};

	const nextCard = () => {
		showCardBack = false;
		if (flashcardIndex === countryData.length - 1) {
			flashcardIndex = 0;
		} else {
			flashcardIndex += 1;
		}
	};
</script>

<main>
	<h1>Flip the Card to Reveal Answer</h1>
	<!-- FLASHCARD -->
	<div class="flip-box">
		<div class="flip-box-inner" class:flip-it={showCardBack}>
			<Flashcard {clue} {answer} {showCardBack} />
		</div>
	</div>

	<!-- BUTTONS -->
	<div id="btn-cont">
		<button class="arrow-btn" on:click={prevCard}>&#8592;</button>

		<button on:click={toggleShowBack}>
			{showCardBack ? 'Hide Answer' : 'Show Answer'}
		</button>

		<button class="arrow-btn" on:click={nextCard}>&#8594;</button>
	</div>
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
	}

	/* This container is needed to position the front and back side */
	.flip-box-inner {
		position: relative;
		width: 100%;
		height: 100%;
		text-align: center;
		transition: transform 0.8s;
		transform-style: preserve-3d;
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
	}

	button {
		background-color: var(--primary);
		padding: 10px 10px;
		color: rgb(0, 0, 0);
		cursor: pointer;
		margin: 5px;
		line-height: 0.7;
		font-weight: 800;
	}

	button:active {
		background-color: var(--primary-hover);
	}
</style>
