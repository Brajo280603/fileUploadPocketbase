<script>
    import PocketBase from 'pocketbase'

    const pb = new PocketBase('http://localhost:8090')

    let file;
    let fileName;

    async function uploadFile(){
        const formData = new FormData()

        if(!!file && !!fileName){
            file = file['0']
            formData.append('file',file)
            formData.append('name',fileName)

            // console.log(formData.entries())
            const createdRecord = await pb.collection('files').create(formData)

            console.log(createdRecord)
            alert(`${createdRecord.name} is saved....`)
        }
       

    }

</script>

<main class="flex justify-center items-center h-full w-full flex-col gap-10">
    <div class="flex gap-5 items-center">
        <input
            bind:value={fileName}
            class="input p-1 px-4"
            placeholder="Enter name here"
            type="text" name="file Name" id="">

        <input 
        bind:files={file}
        type="file" name="file" id="">

    </div>

    <button type="button" class="btn variant-ghost" on:click={uploadFile}>
        Submit
    </button>


</main>