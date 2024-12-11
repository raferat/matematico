<script lang="ts">
    import Button from "$lib/Button.svelte";
import Generator from "$lib/Generator.svelte";

    let started = $state(false);
    

    function startGame() {
        started = true;   
    }
</script>

<main>
    <div id="gamewrapper">
        {#if started}
            <Generator timeout={8} />
            <!--<Generator timeout={2} />
            <Generator timeout={3} />
            <Generator timeout={4} />-->
        {:else}
            <Button onclick={startGame}>Start</Button>
        {/if}
    </div>
    
</main>

<style lang="scss">
    @use 'sass:color';

    main {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        

        #gamewrapper {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 20px;
            padding: 20px;

            width: 600px;
            height: 400px;
            background-color: #181825;
            border-radius: 20px;
            box-shadow: 0px 0px 20px color.mix(#313244, #cba6f7, 95%);
        }
    }
</style>
