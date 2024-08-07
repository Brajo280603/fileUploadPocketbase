<script>
	import PocketBase from 'pocketbase'
	import {onMount} from 'svelte'

	const pb = new PocketBase('http://localhost:8090')
	let listItem

	onMount(async()=>{
		listItem = await pb.collection('files').getFullList({
			sort:'-created',
		})
	})
	
</script>

<main style="height: 100%;width:100%;">

	{#if !!listItem}
		{#await listItem}
			<p>loading</p>
		{:then items}
            <ul class="list gap-5 flex flex-col px-12 pt-12">
			    {#each items as item}
                    <li>
                        <p class="flex justify-between w-full gap-5"><span class="text-orange-300 font-bold ">{!!item.name?item.name:"NA"}</span> <span>{item.file}</span> <span class="text-gray-500"> created : {new Date(item.created)}</span> <a href="http://localhost:8090/api/files/{item.collectionId}/{item.id}/{item.file[0]}" class="btn variant-ghost" target="_blank">SHOW</a></p>
                    </li>
			    {/each}
            </ul>
		{/await}		
	{/if}


</main>