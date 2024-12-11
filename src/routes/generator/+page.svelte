<script lang="ts">
    import Generator from "$lib/Generator.svelte";

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
        
        

        <div id="gen">
            <Generator />
        </div>
        
        
    </div>
    
</main>

<style lang="scss">

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
        grid-template-columns: 1fr 1fr;
        grid-template-rows: auto;
        grid-auto-rows: 1fr;

        justify-items: center;
        align-content: center;
        

        border: 1px solid #313244;
        border-radius: 20px;


        #gen {
            grid-column: 1/3;
        }
    }
</style>