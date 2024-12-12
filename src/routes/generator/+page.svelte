<script lang="ts">
    import Generator from "$lib/Generator.svelte";
    import Slider from "$lib/Slider.svelte";

    const GameStates = {
        pregame: 0,
        playing: 1,
        postgame: 2,
    }

    let timeout = $state(2);
    let gamestate = $state(GameStates.pregame);
     
</script>
<main>
    <div id="content">
        {#if gamestate === GameStates.pregame}
        <label for="timeout">Rychlost:</label>
        <Slider id="timeout" min="1" max="5" step="0.1" bind:value={timeout} />
        <div></div>
        <div>({timeout})</div>
        {:else if gamestate === GameStates.playing}
        <div id="gen">
            <Generator {timeout} />
        </div>
        {:else}
        <h1>ssss</h1>
        {/if}
        

        
        
        
    </div>
    
</main>

<style lang="scss">

    label {
        margin: auto;
    }

    main {
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        padding: 20px;
    }

    #content {
        width: 400px;
        height: 400px;
        padding: 20px;

        display: grid;
        grid-template-columns: 0.3fr 1fr;
        grid-template-rows: auto;
        gap: 20px;
        //grid-auto-rows: 1fr;

        justify-items: center;
        align-content: center;
        

        border: 2px solid #313244;
        border-radius: 20px;


        #gen {
            grid-column: 1/3;
        }
    }
</style>