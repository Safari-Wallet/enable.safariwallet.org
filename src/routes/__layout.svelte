<script context="module">
    import { browser, dev } from '$app/env';
    export const hydrate = dev;
    export const router = browser;
    export const prerender = true;
</script>

<script>
    import '$lib/global.scss';
</script>

<slot />
