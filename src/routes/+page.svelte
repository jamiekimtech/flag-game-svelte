<script>
	import '@picocss/pico/css/pico.min.css';
</script>

<main>
	<h1>Choose Today's game</h1>
	<div class="container">
		<div class="button">
			<a href="/flipcardgame">
				<div class="text-image-wrapper">
					<p>Flip<br /> the Card</p>
					<img alt="Flip the Card" />
				</div>
			</a>
		</div>

		<div class="button">
			<a href="/multichoicegame">
				<div class="text-image-wrapper">
					<p>Multiple<br /> Choice</p>
					<img alt="Flip the Card" />
				</div>
			</a>
		</div>
	</div>
</main>

<style>
	:root[data-theme='dark'] {
		--primary: #24d5a3;
		--primary-hover: #dc479e;
	}
	:root[data-theme='light'] {
		--primary: #82d5bd;
		--primary-hover: #d69fbf;
	}

	.container {
		display: flex;
		flex-direction: row;
		justify-content: center;
		gap: 30px;
	}

	.button {
		position: relative;
	}

	.text-image-wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.button p {
		position: absolute;
		top: 30px;
		left: -10px;
		z-index: 5;
		color: white;
		font-size: 30px;
		font-weight: 900;
		-webkit-text-stroke-width: 2.1px;
		-webkit-text-stroke-color: black;
		letter-spacing: -2.5px;
		line-height: 0.8;
		width: 110px;
	}
	img {
		height: 90px;
		width: 90px;
		margin: 10px auto;
		border-radius: 10px;
		outline: none;
		box-shadow: 10px 20px 30px rgba(0, 0, 0, 0.1);
		background-color: transparent;
		border: none;
		overflow: hidden;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	img:before {
		content: '';
		height: 100%;
		width: 100%;
		font-size: 25px;
		letter-spacing: 6px;
		font-weight: 700;
		padding: 32px 0;
		color: #fcfcfc;
		background-color: rgba(255, 255, 255, 0.06);
		backdrop-filter: blur(25px);
		z-index: 1;
	}
	img:after {
		content: '';
		height: 500px;
		width: 500px;
		margin: -200px -90px;
		z-index: -1;
		background-image: conic-gradient(
			#24d5a3,
			#dc479e,
			#dc479e,
			#dc479e,
			#dc479e,
			#dc479e,
			#2decb7,
			#dc479e,
			#dc479e,
			#dc479e,
			#dc479e
		);
	}

	.button:hover img:after {
		animation: spin 1.8s linear infinite;
	}
	@keyframes spin {
		100% {
			transform: rotate(360deg);
		}
	}
	h1 {
		margin-bottom: 20px;
	}
	main {
		margin: 30px;
	}
</style>
