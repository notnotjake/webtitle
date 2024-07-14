<script>
	import { page } from '$app/stores'
	import { goto } from '$app/navigation'
	
	let title = ""
	
	// Check url params for existing title
	$: existingTitle = $page.url.searchParams.get("title")
	$: if (existingTitle) {
		title = decodeURIComponent(existingTitle)
	}
	
	// Update url params when input changes
	const updateSearchParams = () => {
		const searchParams = new URLSearchParams($page.url.searchParams)
		searchParams.set('title', encodeURIComponent(title))
		goto(`?${searchParams}`, {replaceState: true, keepFocus: true})
	}
	
	$: {
		if (typeof document !== 'undefined') {
			document.title = title
		}
	}
	
</script>

<svelte:head>
	<title>{title}</title>
</svelte:head>

<div class="page-wrapper">
	
	<div class="wrapper">
		<h1>Name this Page</h1>
		<p>Use this to create named folders in Orion</p>
		
		<input type="text" id="title" name="title" minlength="1" maxlength="50" placeholder="Untitled Folder" bind:value={title} on:change={updateSearchParams}>
	</div>
	
</div>

<style src="./_page.scss" lang="scss" ></style>