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

	function handlePreviousClick() {
		dispatch('previousPage');
	}


</script>

<div class="block">
	ขณะที่คุณเดินโซเซผ่านหมอก คุณสังเกตเห็นแสงเรืองรองอยู่ข้างหน้า คุณเดินไปใกล้และพบลูกกลมเล็กๆ ที่เรืองแสง มันให้ความรู้สึกคุ้นเคยอย่างประหลาด ใช่แล้วมันคือความทรงจำที่มีค่าที่สุดในวัยเด็กของคุณ มันคืออะไร?
</div>
<div class="content" style="height: {contentHeight}px; width: {contentWidth}px;">
	<button on:click={handlePreviousClick}></button>
	<div class="space"></div>
	<button on:click={() => handleClick(0, 1)}></button>
</div>

<style>
	.content {
		display: grid;
		z-index: 1;
		justify-items: center;
		align-items: center;
		position: relative;
		grid-template-columns: 30% 25% 45%;
	}
	button {
		width: 100%;
		height: 100%;
		background: none;
		border: none;
		object-fit: contain;
	}
	.space {
		height: 100%;
		width: 100%;
	}
</style>
