<script context='module'>
	import {lookup} from 'app/data/groups';
	import {parseCSV} from 'app/utils/domain';

	export function preload({ params: {id}, query }) {
		return this.fetch(lookup[id].url)
		.then(r => r.text())
		.then(parseCSV(id))
		.then(data => ({data, id}))
	}
</script>

<script>
	import * as _ from 'lamb';

	import IdIndex from '@svizzle/time_region_value/src/routes/[id]/index.svelte';

	import types from 'app/data/types';
	import {lookupStore} from 'app/stores/data';
	import {
		availableYearsStore,
		resetSelectedYear,
	} from 'app/stores/selection';

  export let data;
	export let id;

	$: id && resetSelectedYear();
	$: ({availableYears, title} = $lookupStore[id] || {});
	$: $availableYearsStore = availableYears;

	// FIXME can't, `lookupStore` is now a `derived`
	// $: data && lookupStore.update(_.setPath(`${id}.data`, data));
</script>

<svelte:head>
	<title>EURITO CSVs - {title}</title>
</svelte:head>

<IdIndex
	{data}
	{id}
	{lookupStore}
	{types}
/>
