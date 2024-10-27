<script>
	import { createEventDispatcher } from "svelte";
	export let contentHeight;
	export let contentWidth;

	const dispatch = createEventDispatcher();

	/**
     * @param {number | undefined} [additionalPoint]
     * @param {number} [pageIncrement]
     */
	 function handleClick(additionalPoint, pageIncrement) {
		dispatch('nextPage', { additionalPoint, pageIncrement });
	}

</script>

<div class="content" style="height: {contentHeight}px; width: {contentWidth}px;">

	<div class="space"></div>

	<div class="block">
		หลังจากคุณกวาดตาไปรอบๆคุณพบกับ ร่างๆหนึ่งปรากฏต่อหน้าคุณ เป็นเด็กสาวที่มีรอยยิ้มอ่อนโยน ในมือของเธอ เธอถือลูกแก้วเรืองแสงขนาดเล็ก
	</div>
	<div class="space"></div>
	<div class="as">
			<button on:click={() => handleClick(0, 1)}>คุณตัดสินใจ จะตามเธอเข้าไปในป่าลึกหวังว่ามันจะช่วยนะ</button>
			<button on:click={() => handleClick(0, 2)}>คุณเลือกที่จะไม่ตามเธอแต่คุณก็ยังไม่รู้จักสถานที่แห่งนี้</button>
			<div class="space"></div>
			<div class="space"></div>
	</div>

	<div class="space"></div>

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
		grid-template-rows: 45% 45% 10%;
		width: 100%;
	}
	.as {
		height: 100%;
		width: 60%;
		display: grid;
		align-items: center;
		grid-template-rows: 1fr 1fr 1fr 1fr;
		gap: 5%;
		/* background-color: aqua;	 */
	}
	.as button {
		font-family: 'CloudLoop';
		font-size: 14px;
		color: darkslategrey;
		height: 100%;
		width: 100%;
		border-radius: 20px;
		border: 1px;
		background-color: #ffffff;
	}
	.space {
		height: 100%;
	}

</style>
