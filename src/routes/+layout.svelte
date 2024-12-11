<script lang="ts">
    import { page } from '$app/stores';
    import { expoInOut } from 'svelte/easing';
    import { Tween } from 'svelte/motion';

    let { children } = $props();

    let position = new Tween(-290, {
        duration: 250,
        easing: expoInOut,
    });

    let value = $derived($page.url.pathname);

    $effect(()=>{
        if (value === "/") {
            position.set(-290);
        } else if (value === "/generator/") {
            position.set(0);
        } else {
            position.set(290);
        }
    });
</script>


<div class="wrapper">
    <header>
        <nav>
            <ul>
                <li><a href="/">Matematico</a></li>
                <li><a href="/generator/">Generator</a></li>
                <li><a href="/game/">Hra</a></li>
            </ul>
            
            <div id="marker" style="left: calc(50% + {position.current}px)">
                <div></div>
            </div>
        </nav>
    </header>
    <div>
        {@render children()}
    </div>
</div>

<style lang="scss">
    :root {
        color-scheme: dark;
    }

    :global(*) {
        box-sizing: border-box;
    }

    :global(body) {
        border: none;
        margin: 0;
        padding: 0;
        height: 100vh;
        width: 100vw;

        background-color: #1e1e2e;
        color: #cdd6f4;
    }

    .wrapper {
        height: 100vh;
        width: 100vw;
        display: grid;
        grid-template-rows: auto 1fr;

    }

    #marker {
        position: absolute;
        transform: translateX(-50%);
        top: calc(73px - 0.9em);

        div {
            
            height: 0;
            border-left: 0.55em solid transparent;
	        border-right: 0.55em solid transparent;
	        border-bottom: 0.9em solid #89dceb;
        }
    }

    header {
        display: flex;
        justify-content: center;
        align-items: center;

        nav {
            background-color: #11111b;
            padding: 0 20px;
            border-bottom-left-radius: 20px;
            border-bottom-right-radius: 20px;
            box-shadow: 2px 2px 2px #89dceb;

            ul {
                padding: 0;
                margin: 0;
                display: flex;
                gap: 90px;
                justify-content: center;
                align-items: center;


                li {
                    list-style: none;


                    a {
                        text-decoration: none;
                        color: #cdd6f4;
                        font-size: 18pt;
                        font-weight: 600;
                        width: 200px;
                        text-align: center;
                        display: inline-block;
                        transition: 250ms ease-in-out;
                        padding: 20px 0;

                        &:hover {
                            color: #89dceb;
                        }
                    }
                }
            }
        }
    }
</style>

