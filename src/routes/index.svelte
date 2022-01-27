<script>
    import Prompt from '$lib/components/Prompt.svelte';
    import { onMount } from 'svelte';
    import confetti from 'canvas-confetti';

    let enabled = false;

    onMount(() => {
        setInterval(() => {
            const isEnabled = typeof window.ethereum !== `undefined`;
            if (!!isEnabled == !enabled) {
                enabled = isEnabled;
                if (!!enabled) {
                    setTimeout(() => {
                        confetti({
                            origin: {
                                y: .5,
                            },
                            particleCount: 100,
                            spread: 70,
                            zIndex: 99,
                        });
                    }, 500);
                }
            }
        }, 100);
    });

    const PAGE_TITLE = `Enable Safari Wallet`;
    const CANONICAL_URL = `https://enable.safariwallet.org`;
</script>

<svelte:head>
    <title>{PAGE_TITLE}</title>
    <meta property="og:title" content={PAGE_TITLE}>
    <meta name="twitter:title" content={PAGE_TITLE}>
    <link rel="canonical" href={CANONICAL_URL}>
    <meta property="og:url" content={CANONICAL_URL}>
    <meta name="twitter:url" content={CANONICAL_URL}>
</svelte:head>

<main class="container">
    <div>
        {#if enabled === false}
            <div class="flex">
                <img src="/img/safari-wallet-icon.png" alt="">
                <img src="/img/puzzle-large-blue.svg" alt="">
                <img src="/img/safari-icon.png" alt="">
            </div>
            <img src="/img/menu.png" alt="" width="270">
            <div class="flex">
                <ol class="list">
                    <li><p>Tap on <img class="inline" src="/img/sf-aa.png" alt="" width="23" height="16"> <img class="inline" src="/img/sf-puzzle.png" alt="" width="21" height="16"></p></li>
                    <li><p>Tap "Manage Extensions"</p></li>
                    <li><p>Enable <img class="inline" src="/appicon.png" alt="" width="22" height="22"> Extension</p></li>
                </ol>
            </div>
            <Prompt />
        {:else}
            <h1><img class="inline" src="/img/checkmark.svg" alt="" width="28" height="28">&nbsp;&nbsp;Safari Extension Enabled</h1>
            <h2>Suggested Dapps</h2>
            <button class="button">
                Open Safari Wallet App
            </button>
        {/if}
    </div>
</main>

<style>
    .container {
        display: flex;
        justify-content: center;
        text-align: center;
        width: 100%;
    }
    .flex {
        align-items: center;
        display: flex;
        justify-content: center;
    }
    .list {
        color: #434343;
        font-size: 24px;
        line-height: 14px;
        padding-left: 0;
        text-align: left;
    }
    img.inline {
        margin-bottom: -2px;
    }
    .button {
        background-color: #0b84ff;
        border: 0;
        border-radius: 8pt;
        color: #fff;
        cursor: pointer;
        font-size: 16px;
        font-weight: 600;
        line-height: 22px;
        padding: 14px 25px;
    }
</style>
