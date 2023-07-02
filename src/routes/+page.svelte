<script>
	import '@picocss/pico/css/pico.min.css';
	let images = [
		{
			buttonImage: 'https://cdn.pixabay.com/photo/2016/08/13/17/59/background-1591229_1280.jpg'
		}
	];

	let theme = 'dark';

	const toggleTheme = function () {
		theme = theme === 'dark' ? 'light' : 'dark';
		document.documentElement.setAttribute('data-theme', theme);
	};
</script>

<main>
	<fieldset>
		<label for="switch">
			<input
				type="checkbox"
				id="switch"
				name="switch"
				role="switch"
				checked
				on:change={toggleTheme}
			/>
			{theme.toUpperCase()} THEME
		</label>
	</fieldset>
	<h1>Choose Today's game</h1>
	<a href="/flipcardgame"><img class="button" src={images[0].buttonImage} alt="Flip the Card" /></a>
	<a href="/multichoicegame"
		><img class="button" src={images[0].buttonImage} alt="Multi Choice Game" /></a
	>

	<p>Give me feedback at jamiekimtech313@gmail.com</p>
</main>

<style>
	img {
		height: 90px;
		width: 90px;
		margin: 10px;
	}
	h1 {
		margin-bottom: 20px;
	}
	main {
		margin: 30px;
		text-align: center;
	}

	p {
		margin-top: 30px;
	}
</style>
