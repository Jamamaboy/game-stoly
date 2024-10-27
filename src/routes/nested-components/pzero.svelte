<script>
	import { createEventDispatcher } from "svelte";
	import { browser } from '$app/environment'; // Import the 'browser' object
	import audioFile from '../../public/audio/Ghost Party by The Piano Says.mp3';

	export let contentHeight;
	export let contentWidth;

	const dispatch = createEventDispatcher();

	/**
	 * @type {HTMLAudioElement}
	 */
	let audio;
	let isAudioPlaying = false;

	// Only initialize audio if we are in the browser
	if (browser) {
		audio = new Audio(audioFile);
		audio.loop = true; // Enable loop for the audio
	}

	/**
	 * @param {number | undefined} [additionalPoint]
	 * @param {number} [pageIncrement]
	 */
	function handleClick(additionalPoint, pageIncrement) {
		if (browser && !isAudioPlaying) {
			audio.play().catch(err => {
				console.error("Failed to play audio:", err);
			}); // Play the audio
			isAudioPlaying = true; // Set the audio state as playing
		}
		dispatch('nextPage', { additionalPoint, pageIncrement });
	}
</script>

<div class="Block">
	<p>คุณตื่นขึ้นมาด้วยอาการมึนงง หลงอยู่ในป่าที่ปกคลุมไปด้วยหมอก อากาศเย็นและชื้น มีเพียงเสียงลมพัดแผ่วเบาจากระยะไกลเท่านั้นที่ได้ยิน</p>
</div>
<div class="content" style="height: {contentHeight}px; width: {contentWidth}px;">
	<button
		on:click={() => handleClick(0, 1)}
		aria-label="Continue to the next page"
		disabled={isAudioPlaying}>
	</button>
</div>

<style>
	@font-face {
		font-family: 'CloudLoop';
		src: url('./font/CloudLoop-Regular.otf') format('opentype');
		font-weight: normal;
		font-style: normal;
		font-display: swap;
	}

	.content {
		display: grid;
		z-index: 1;
		justify-items: center;
		align-items: center;
	}

	button {
		font-size: 1px; /* Consider removing or changing to make the button more accessible */
		width: 100vh;
		height: 100vh;
		background: none;
		border: none;
		cursor: pointer; /* Change cursor to pointer for better UX */
		/* Optional hover effects */
		transition: background-color 0.3s;
	}

	button:hover {
		background-color: rgba(255, 255, 255, 0.1); /* Change to any color you prefer */
	}

	.Block {
		z-index: 1;
	}
</style>

