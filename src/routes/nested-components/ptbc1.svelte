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

<div class="block">
	คุณพยายามนึกถึงเรื่องราวก่อนหน้า ถึงสาเหตุที่คุณมาโผล่ในสถานที่แห่งนี้ได้ยังไง แต่ยิ่งคุณพยายามนึกเท่าไหร่ก็นึกไม่ออก
</div>
<div class="content" style="height: {contentHeight}px; width: {contentWidth}px;">
	<div class="space"></div>
	<button on:click={() => handleClick(0, 1)}>ก</button>
</div>

<style>
	.content {
		display: grid;
		z-index: 1;
		justify-items: center;
		align-items: center;
		position: relative;
		grid-template-columns: 50% 50%;
	}
	button {
		width: 100%;
		height: 100%;
		z-index: 1;
		background: none;
		border: none;
		object-fit: contain;
	}
	.space {
		height: 100%;
		width: 100%;
	}
</style>
