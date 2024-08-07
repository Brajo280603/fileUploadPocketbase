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

    async function deleteFile(file){
        if(confirm(`are you sure to delete ${file.file['0']}`)){
            await pb.collection('files').delete(file.id);
            alert(`${file.name} is deleted successfully...`)
            listItem = await pb.collection('files').getFullList({
                sort:'-created',
            })
        }
        
    }

</script>

<main style="height: 100%;width:100%;">

	{#if !!listItem}
		{#await listItem}
			<p>loading</p>
		{:then items}
            <ul class="list gap-5 flex flex-col px-12 pt-12">
			    {#each items as item}
                    <li>
                        <p class="flex justify-between w-full"><span class="text-orange-300 font-bold ">{!!item.name?item.name:"NA"}</span> <span>{item.file}</span> <span class="text-gray-500"> created : {new Date(item.created)}</span> <button class="btn variant-ghost" on:click={deleteFile(item)}>DELETE</button></p>
                    </li>
			    {/each}
            </ul>
		{/await}		
	{/if}


</main>