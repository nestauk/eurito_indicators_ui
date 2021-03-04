<script>
	import {onMount} from 'svelte';
	import ScreenGauge, {screen}
		from '@svizzle/ui/src/gauges/screen/ScreenGauge.svelte';

	import Nav from 'app/components/Nav.svelte';
	import {fontScaling} from 'app/stores/fontScaling';

	const dev = process.env.NODE_ENV === 'development';

	export let segment;

	let rootStyle;
	let defaultFontSize;

	onMount(() => {
		const root = document.documentElement;
		defaultFontSize = window.getComputedStyle(root).fontSize;
		rootStyle = root.style;
	})

	// set document root element font size so that `rem` units work
	$: rootStyle
		&& (rootStyle.fontSize = `calc(${defaultFontSize} * ${$fontScaling})`);
</script>

<ScreenGauge
	bands={[45, 90, 135, 180]}
	devMode={dev}
/>

{#if $screen?.sizeFlags.medium}
	<header>
		<Nav {segment} screen={$screen}/>
	</header>
{/if}

<main>
	<slot></slot>
</main>

{#if !$screen?.sizeFlags.medium}
	<header class='small'>
		<Nav {segment} screen={$screen}/>
	</header>
{/if}

<style>
	header {
		height: var(--dim-header-height);
		width: 100%;
		padding: 0 var(--dim-padding);
		border-bottom: 1px solid var(--color-main-lighter);
	}

	header.small {
		border-top: 1px solid var(--color-main-lighter);
		border-bottom: none;
	}

	main {
		height: var(--dim-main-height);
		width: 100%;
		overflow: hidden;
	}
</style>
