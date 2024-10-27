<script lang="ts">

	import RED from '../../public/Img/GO/RED.jpg';
	import YELLO from '../../public/Img/GO/YELLO.jpg';


	import { onMount } from "svelte";
	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	export let point: number[];
	let totalPoints = 0;
	let gift = "";

	$: calculateTotalPoints();
	$: determineGift();

	function calculateTotalPoints() {
		totalPoints = point.reduce((acc, curr) => acc + curr, 0);
		console.log(totalPoints);
	}
	function determineGift() {
		if (totalPoints >= 0 && totalPoints <= 1) {
			gift = RED;
		} else if (totalPoints > 1 && totalPoints <= 2) {
			gift = YELLO;
	}
	}

	function reset() {
		window.location.reload();
	}

	function downloadImage(gift: string) {
		const link = document.createElement('a');
		link.href = gift;
		link.download = `gift.jpg`;
		document.body.appendChild(link);
		link.click();
		document.body.removeChild(link);
	}

	onMount(() => {
	});

</script>

<div class="container">

	<img src={gift} alt="{gift}" />

	<div class="controls">
		<button on:click={reset}>ReStart Game</button>
		<button on:click={() => downloadImage(gift)}>Download Image</button>
	</div>

</div>

<style>

	@font-face {
		font-family: 'CloudLoop';
		src: url('./font/CloudLoop-Regular.otf') format('opentype');
		font-weight: normal;
		font-style: normal;
		font-display: swap;
	}
	.container {
		display: grid;
		grid-template-rows: 90% 10%;
		align-items: center;
		justify-items: center;
		height: 100%;
		width: auto;
		object-fit: contain;
	}

	img {
		max-width: 100%;
		height: auto;
	}

	.controls {
		display: grid;
		grid-template-columns: 1fr 1fr;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		padding-top: 5%;
	}

	button {
		font-family: 'CloudLoop';
		font-size: 16px;
		min-width: 60%;
		padding: 5px;
		padding-left: 10%;
		padding-right: 10%;
		color: black;
		border: 1px solid black;
		border-radius: 20px;
		background-color: white;
		transition: background-color 0.3s;
		align-self: center;
		justify-self: center;
	}
</style>
