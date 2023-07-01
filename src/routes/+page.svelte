<script>
	let images = [
		{
			buttonImmage: 'https://cdn.pixabay.com/photo/2016/08/13/17/59/background-1591229_1280.jpg'
		}
	];
</script>

<main>
	<h1>Choose Today's game</h1>
	<a href="/flipcardgame"><img class="button" src={images[0].buttonImmage} alt="Flip the Card" /></a
	>
	<a href="/multichoicegame"
		><img class="button" src={images[0].buttonImmage} alt="Multi Choice Game" /></a
	>
</main>

<style>
	.button {
		width: 180px;
		height: 180px;
	}
</style>
