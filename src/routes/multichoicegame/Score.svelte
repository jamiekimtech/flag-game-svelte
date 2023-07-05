<script>
	import { percentStore } from './store.js';
	export let size = 200;
	export let bgColor = 'var(--primary)';
	export let fgColor = 'var(--primary-hover)';
	export let percent;

	$: {
		percent = $percentStore;
	}

	$: viewBox = `0 0 ${size} ${size}`;

	$: radius = size / 2;
	$: halfCircumference = Math.PI * radius;
	$: pieSize = halfCircumference * (percent / 100);
	$: dashArray = `0 ${halfCircumference - pieSize} ${pieSize}`;

	let isOpen = true;
	const closeModal = function () {
		isOpen = !isOpen;
	};

	// Subscribe to percentStore
	$: percentStore.subscribe((value) => {
		percent = value;
	});
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
		<h5>Your score is {percent.toFixed(2)}%.</h5>
	</article>
</dialog>

<style>
	h5 {
		margin-top: 30px;
	}
</style>
