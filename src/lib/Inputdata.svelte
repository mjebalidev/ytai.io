<script>
    import { Configuration, OpenAIApi } from 'openai';
    import TabHeadItem from './TabHeadItem.svelte';
    import TabWrapper from './TabWrapper.svelte';
    import TabHead from './TabHead.svelte';
    import TabContentItem from './TabContentItem.svelte';

    let activeTabValue = 1;
    const handleClick = (tabValue) => () => {
        activeTabValue = tabValue;
    };
    const configuration = new Configuration({
        apiKey: 'ADD YOUR API KEY HERE'
    });
    const openai = new OpenAIApi(configuration);
    let output
    let data
    let pitch = "Write me a pitch presentation for a youtube video about "
    let pitchResult
    const createImage = async () => { 
        const response = await openai.createImage({
            prompt:"Youtube cover for " + data,
            n: 1,
            size: "512x512",
        });
    output = response.data.data[0].url;
    };

    const getCompletion = async () => {
        const response = await openai.createCompletion({
            model: 'text-davinci-002',
            prompt: pitch + data,
            max_tokens: 2000,
            temperature: 0.6
        });
    pitchResult = response.data.choices[0].text;
    };

    const run = async () => {
        await createImage();
        await getCompletion();
    };
</script>

<main>
<div class="inputdata">
    <!-- input field that updates data -->
    <input type="text" bind:value={data} class="textfield" />
    <!-- button that retieves data -->
    <button class="button" on:click={run}>Send</button>
</div>

{#if pitchResult && output}
    <div class="resultData">
    <TabWrapper>
        <TabHead>
         <TabHeadItem id={1} on:click={handleClick(1)}>Pitch result</TabHeadItem>
         <TabHeadItem id={2} on:click={handleClick(2)}>Image result</TabHeadItem>
       </TabHead>
       <TabContentItem id={1} {activeTabValue}>{pitchResult}</TabContentItem>
       <TabContentItem id={2} {activeTabValue}><img src={output}/></TabContentItem>
    </TabWrapper>
    </div>
{/if}
</main>

<style>
    .inputdata{
        height: 10em;
        padding: 1.5em;
    }
    .button{
        color: rgb(139, 41, 19);
        border-color: rgb(79, 7, 7);
        height: 3em;
    }
    .button:hover{
        filter: drop-shadow(0 0 1em #9a7e7eaa);
    }
    .textfield{
        height: 2em;
    }
    .textpitch{
        color: rgb(139, 41, 19);
        font-size: medium;
    }
</style>
