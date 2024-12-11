<script lang="ts">
    import { onDestroy, onMount } from "svelte";
    import { sineInOut } from "svelte/easing";
    import { Tween } from "svelte/motion";
    import { fade } from "svelte/transition";
    

    let currentNumber = $state(-1);
    let seqidx = $state(0);

    let { timeout = 2, onEnd = () => {} } : { timeout?: number, onEnd?: () => void } = $props();

    function shuffleArray(array: any[]) {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
        }

        return array;
    }

    function generateSequence() {
        let result = []
        for(let i = 1; i < 13+1; i++) {
            for(let j = 0; j < 3; j++) {
                result.push(i);
            }
        }

        return shuffleArray(shuffleArray(shuffleArray(result))).slice(0,25);
    }

    const tween = new Tween(0, {easing: sineInOut, duration: timeout*1000});
    let transitionHandler = $state({});

    function startGame() {
        const seq = generateSequence();
        
        currentNumber = seq[seqidx++];
        tween.set(100.1);

        let timer = setInterval(() => {
            if (seqidx >= seq.length) {
                onEnd();
                clearInterval(timer);
                return;
            }
            currentNumber = seq[seqidx++];
            tween.set(0, {duration: 0}).then(() => {
                tween.set(100.1);
            });

            transitionHandler = {};
        }, timeout * 1000);

        
        

        onDestroy(() => {
            clearInterval(timer);
        });
    }

    

    onMount(startGame);
</script>

<div class="wrapper">
    
    {#key transitionHandler}
        <h3 in:fade={{duration:200}}>{currentNumber}</h3>    
    {/key}
    
    
    <div class="progressbar">
        <div class="progress" style="clip-path: inset(0 {100 - tween.current}% 0 0);"></div>
    </div>
</div>

<style lang="scss">
    .wrapper {
        display: flex;
        gap: 20px;
        flex-direction: column;
        justify-content: center;
        align-items: center;

    }

    h3 {
        font-size: 90pt;
        margin: 0;
        color: #cdd6f4;
    }

    .progressbar {
        height: 30px;
        width: 220px;
        padding: 5px;
        border-radius: 200px;
        border: 2px solid #89dceb;
    }

    .progress {
        height: 100%;
        width: 100%;
        border-radius: 20px;
        background-color: #89dceb;
        clip-path: inset(0 20px 0 2px);
    }
</style>