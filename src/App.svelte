<script>
	import { onMount } from 'svelte';
	import VirtualList from './VirtualList.svelte';
	import ListItem from './ListItem.svelte';

	let titleSearchTerm = "";
	let cgroupSearchTerm = "";
	let items = [];
	let groups = [];
	let selected = "[UK] SPORTS";

	onMount(async () => {
		const res = await fetch("./data.json");
		items = await res.json();

		const res_groups = await fetch("./groups.txt");
		let grouptext = await res_groups.text();
		groups = grouptext.split('\n');
		
	});

	$: filteredList = items.filter(item => item.title.indexOf(titleSearchTerm) !== -1)
	.filter(item => item.cgroup.indexOf(cgroupSearchTerm) !== -1);
	
  let start;
  let end;
	
</script>

<h1>Talant IPTV</h1>

<select bind:value={cgroupSearchTerm}>
	{#each groups as value}<option {value}>{value}</option>{/each}
</select>
<br />

Filter Group: <input bind:value={cgroupSearchTerm} />
{cgroupSearchTerm}<br />
Filter Title: <input bind:value={titleSearchTerm} />
{titleSearchTerm}

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
