<script>
	let theme = 'dark';

	const toggleTheme = function () {
		theme = theme === 'dark' ? 'light' : 'dark';
		document.documentElement.setAttribute('data-theme', theme);
	};
</script>

<div>
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

	<slot />
	<p>Give me feedback at <br />jamiekimtech313@gmail.com</p>
</div>

<style>
	div {
		text-align: center;
		margin-top: 15px;
	}

	p {
		margin-top: 50px;
	}
</style>
