<script lang="ts">
    import type { Snippet } from "svelte";

    let { children, onclick } : { children?: Snippet<[]> , onclick?: ()=>void} = $props();
    
</script>

<button {onclick}>
    {@render children?.()}
</button>

<style lang="scss">
    button {
        height: 40px;
        min-width: 100px;
        border-radius: 20px;
        
        border: 2px solid #89dceb;
        background: none;
        outline: none;
        cursor: pointer;

        font-size: 12pt;

        transition: 250ms cubic-bezier(0.445, 0.05, 0.55, 0.95);
    }

    button:hover {
        font-size: 13pt;
        color: #89dceb;
    }
</style>

