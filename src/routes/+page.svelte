<script lang="ts">
    import { dev } from '$app/environment';

    let page = 0;
    let point = [0];
    let contentHeight = 0;
    let contentWidth = 0;

    let history = [1];

    // Import nested components
    import Pzero from './nested-components/pzero.svelte';
    import Ptbc1 from './nested-components/ptbc1.svelte';
    import Ptbc3 from './nested-components/ptbc3.svelte';
    import Ptbc4 from './nested-components/ptbc4.svelte';
    import Ptbc5 from './nested-components/ptbc5.svelte';
    import Pn from './nested-components/pn.svelte';
    import PEng from './nested-components/pENG.svelte';

    // Import images and videos
    import p0 from '../public/Img/0.jpg';
    import p1 from '../public/Img/1.jpg';
    import mp2 from '../public/Img/2.mp4'; // Make sure this file exists
    import p3 from '../public/Img/3.jpg';
    import p4 from '../public/Img/4.jpg';
    import mp5 from '../public/Img/5.mp4';

    // Page mappings
    const page_zero = [0];
    const page_tbc1 = [1];
    const page_n = [2];
    const page_tbc3 = [3];
    const page_tbc4 = [4];
    const page_tbc5 = [5];
    const page_ENG = [6];

    function handleImageLoad(event: { target: any; }) {
        const video = event.target;
        contentHeight = video.videoHeight; // Use video properties
        contentWidth = video.videoWidth;
    }

    function handleNextPage(event: { detail: { additionalPoint: any; pageIncrement: any; }; }) {
        const { additionalPoint, pageIncrement } = event.detail;

        if (additionalPoint > 0) {
            point.push(additionalPoint);
        }

        let nextPage;
        switch (page) {
            case 7:
                nextPage = 9;
                break;
            case 13:
                nextPage = 15;
                break;
            case 36:
                nextPage = 38;
                break;
            default:
                nextPage = page + pageIncrement;
        }
        history.push(page);
        page = nextPage;
    }
</script>

<main>
    <!-- Zero [0] -->
    {#if page_zero.includes(page)}
        <img src={p0} alt={`Page ${page}`} on:load={handleImageLoad}>
        <Pzero contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage} />
    {/if}

    <!-- TBC [1] -->
    {#if page_tbc1.includes(page)}
        <img src={p1} alt={`Page ${page}`} on:load={handleImageLoad}>
        <Ptbc1 contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage} />
    {/if}

    <!-- N [2] -->
    {#if page_n.includes(page)}
        <video src={mp2} alt={`Page ${page}`} on:loadeddata={handleImageLoad} controls>
            Your browser does not support the video tag.
        </video>
        <Pn contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage} />
    {/if}

    <!-- TBC [3] -->
    {#if page_tbc3.includes(page)}
        <img src={p3} alt={`Page ${page}`} on:load={handleImageLoad}>
        <Ptbc3 contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage}/>
    {/if}

    <!-- TBC [4] -->
    {#if page_tbc4.includes(page)}
        <img src={p4} alt={`Page ${page}`} on:load={handleImageLoad}>
        <Ptbc4 contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage}/>
    {/if}

    <!-- TBC [5] -->
    {#if page_tbc5.includes(page)}
        <img src={mp5} alt={`Page ${page}`} on:load={handleImageLoad}>
        <Ptbc5 contentHeight={contentHeight} contentWidth={contentWidth} on:nextPage={handleNextPage}/>
    {/if}

    <!-- ENG [6] -->
    {#if page_ENG.includes(page)}
        <PEng point={point} />
    {/if}
</main>

<style>
    @font-face {
        font-family: 'CloudLoop';
        src: url('./font/CloudLoop-Regular.otf') format('opentype');
        font-weight: normal;
        font-style: normal;
        font-display: swap;
    }

    html {
        height: 100%;
    }

    img, video {
        z-index: 0;
        max-width: 100dvw;
        max-height: 100dvh;
        width: auto;
        height: auto;
        object-fit: contain;
    }
</style>
