<script lang="ts">
    let { value = $bindable(0), ...props } = $props();
</script>

<input type="range" bind:value {...props} class="slider" />

<style lang="scss">
    .slider {
        -webkit-appearance: none;
        appearance: none;
        width: 100%;
        height: 2px;
        background: transparent;
        outline: none;
        //border: 2px solid #89dceb;
        background-color: #89dceb;
        border-radius: 20px;
        margin: auto;
        //opacity: 0.7;
        //-webkit-transition: .2s;
        //transition: opacity .2s;
    }

    .slider::-webkit-slider-thumb {
        -webkit-appearance: none;
        appearance: none;
        border: none;
        border-radius: 20px;
        width: 20px;
        height: 20px;
        background: #89dceb;
        cursor: pointer;
    }

    .slider::-moz-range-thumb {
        border-radius: 20px;
        width: 20px;
        height: 20px;
        border: 2px solid #89dceb;
        cursor: pointer;
        outline: none;
        appearance: none;
        background-color: #1e1e2e;
    }
</style>
