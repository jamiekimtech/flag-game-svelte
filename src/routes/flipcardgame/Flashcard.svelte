<script>
	export let flag;
	export let countryName;
	export let answerVisible;
</script>

<div class="flip-box-front">
	<div id="image-cont">
		<img src={flag} alt={countryName} />
	</div>
</div>

<div class="flip-box-back" class:conceal-answer={answerVisible}>
	<h2>{countryName}</h2>
</div>

<style>
	/* Position the front and back side */
	.flip-box-front,
	.flip-box-back {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		-webkit-backface-visibility: hidden; /* Safari */
		backface-visibility: hidden;
		box-shadow: -1px 1px 3px rgba(133, 133, 133, 0.761);
	}

	/* Style the front side */
	.flip-box-front {
		/* background-color: #3434341c; */
		color: black;
		display: flex;
		justify-content: center;
		border-radius: 30px;
		border: none;
	}

	@keyframes revealTextSlowly {
		to {
			color: white;
		}
	}

	.conceal-answer {
		animation: revealTextSlowly 0.3s forwards;
	}

	/* Style the back side */
	.flip-box-back {
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: var(--primary);
		font-size: 1.3rem;
		transform: rotateY(180deg);
		border-radius: 30px;
	}

	h2 {
		font-weight: 500;
		color: black;
		margin: 0;
	}

	#image-cont {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	img {
		max-width: 95%;
		max-height: 95%;
	}
</style>
