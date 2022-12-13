<script>
	import { onMount } from 'svelte';
	import VirtualList from './VirtualList.svelte';
	import ListItem from './ListItem.svelte';

	let searchTerm = "";
	let items = [];


	onMount(async () => {
		const res = await fetch("./data.json");
		items = await res.json();
	});

	  // let items = [{lang: 'en', title: 'abcd', link: 'link1', mtype: 'l'},
	// {lang: 'en', title: 'zxyv', link: 'link2', mtype: 's'}]


	$: filteredList = items.filter(item => item.title.indexOf(searchTerm) !== -1);
	
  let start;
  let end;
	
</script>

<h1>Talant IPTV</h1>

Filter Title: <input bind:value={searchTerm} />
{searchTerm}

<div class='container'>
	<VirtualList items={filteredList} bind:start bind:end let:item>
		<ListItem {...item}/>
	</VirtualList>
	<p>showing items {start}-{end}</p>
</div>

<style>
	.container {
		border-top: 1px solid #333;
		border-bottom: 1px solid #333;
		min-height: 200px;
		height: calc(100vh - 15em);
	}
</style>
