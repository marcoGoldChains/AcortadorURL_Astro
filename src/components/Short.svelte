<script>
    //Dominio gratuito: em7j.short.gy
    //Clave de API: sk_FBcY0XnTTXuZ6jpQ 
    
    let url = "";
    let urlResults = "";
    let show = false;

    //Importamos el componente de Svelte para copiar la URL acortada.
    import ClipBoard from "./ClipBoard.svelte";

    //Funcion para copiar la URL acortada.
    const copy = () => {
        const app = new ClipBoard({
            target: document.getElementById('clipboard'),
            props: { urlResults },
        });
        app.destroy();
    }
    
    const fetchUrl = async () => {

        const options = {
            method: 'POST',
            headers: {
                accept: 'application/json',
                'content-type':'application/json',
                Authorization: 'sk_FBcY0XnTTXuZ6jpQ'
            },
            body: JSON.stringify({originalURL: url, domain: 'em7j.short.gy'})
        };
        
        const response = await fetch('https://api.short.io/links', options);
        const data = await response.json();
        console.log(data);
        urlResults = data.shortURL;

        show = true;
    
    }


    const styleInput =
        "bg-gray-200 appeareance-none border-2 border-gray-200 rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500";

    const buttonStyle =
        "bg-purple-500 hover:bg-purple-400 text-white font-bold py-2 px-10 rounded";
</script>

<div class="md:flex md:items-center md-6">
    <div class="md:w-1/3">
        <label for="" class="block text-gray-500 font-bold md:text-right pr-4">
            URL to Shorten
        </label>
    </div>

    <div class="md:w-1/3">
        <input
            type="text"
            placeholder="Example://www.mysite.com"
            bind:value={url}
            class={styleInput}
        />
    </div>
</div>

<div class="md:flex md:items-center mt-5 justify-center">
    <button type="button" class={buttonStyle} on:click={fetchUrl}> Shorten</button>
</div>

{#if show}
<div class="md:flex md:items-center mt-10 justify-center">
    <input bind:value={urlResults} class="text-5xl text-pink-500">
    <button class="{buttonStyle}" on:click={copy}>Copy</button>
    <div id="clipboard"></div>
</div>
{/if}