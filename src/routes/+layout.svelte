<script>
	import MediaQuery from './MediaQuery.svelte';

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
	<MediaQuery query="(max-width: 480px)" let:matches>
		<div class:mobile={matches}>
			<MediaQuery query="(min-width: 490px)" let:matches>
				<div class:tablet={matches}>
					<slot />
				</div>
			</MediaQuery>
		</div>
	</MediaQuery>
</main>
<p>Give me feedback at <br />jamiekimtech313@gmail.com</p>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		text-align: center;
		margin: 5px;
		position: relative;
		padding: 100px;
	}
	fieldset {
		position: absolute;
		top: 40px;
		left: 0;
		right: 0;
		bottom: 0;
		max-height: 30px;
	}
	p {
		margin-top: -100px;
		position: relative;
		text-align: center;
		padding: 30px;
	}
	.mobile {
		transform: scale(0.85);
		transform-origin: center;
	}

	.tablet {
		margin: 50px;
	}
</style>
