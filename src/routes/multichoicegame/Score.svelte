<script>
	export let size = 200;
	export let percent;
	export let bgColor = 'var(--primary)';
	export let fgColor = 'var(--primary-hover)';

	$: viewBox = `0 0 ${size} ${size}`;

	$: radius = size / 2;
	$: halfCircumference = Math.PI * radius;
	$: pieSize = halfCircumference * (percent / 100);
	$: dashArray = `0 ${halfCircumference - pieSize} ${pieSize}`;

	let isOpen = true;
	const closeModal = function () {
		isOpen = !isOpen;
	};
</script>

<dialog open={isOpen}>
	<article>
		<header>
			<a href="#close" aria-label="Close" class="close" on:click={closeModal} />
			Check Your Score!
		</header>
		<svg width={size} height={size} {viewBox}>
			<circle r={radius} cx={radius} cy={radius} fill={bgColor} />
			<circle
				r={radius / 2}
				cx={radius}
				cy={radius}
				fill="none"
				stroke={fgColor}
				stroke-width={radius}
				stroke-dasharray={dashArray}
			/>
		</svg>
	</article>
</dialog>
