<script>
	export let cgroup;
	export let title;
	export let link;


function onClick(event) {
	let alltext = event.target.innerText;
	let words = alltext.split(' -- ');
	let link = words[2];
	navigator.clipboard.writeText(link);
	alert("Copied to clipboard: " + link);
}

</script>

<div class='card'>
	<div class="customAS" on:click={event => onClick(event)}>{cgroup} -- {title} -- {link}</div>
	
</div>
