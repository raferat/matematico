<script lang="ts">
    import { base } from '$app/paths';
    import { page } from '$app/stores';
    import { quadInOut } from 'svelte/easing';
    import { Tween } from 'svelte/motion';
    import { fade, fly } from 'svelte/transition';

    let { children } = $props();

    let position = new Tween(-290, {
        duration: 250,
        easing: quadInOut,
    });

    let pathname = $derived($page.url.pathname);
    $effect(()=>{
        if (pathname === `${base}/`) {
            position.set(-290);
        } else if (pathname === `${base}/generator/`) {
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
                <li><a href="{base}/">Matematico</a></li>
                <li><a href="{base}/generator/">Generátor</a></li>
                <li><a href="{base}/game/">Hra</a></li>
            </ul>
            <div id="marker" style="left: calc(50% + {position.current}px)">
                <svg
                   width="19.843769mm"
                   height="2.2695999mm"
                   viewBox="0 0 19.843769 2.2695999"
                   version="1.1"
                   id="svg5"
                   xmlns="http://www.w3.org/2000/svg">
                  <defs
                     id="defs2" />
                  <g
                     id="layer1"
                     transform="translate(-52.958722,-68.762487)">
                    <path
                       id="path238"
                       style="fill:#89dceb;fill-opacity:1;stroke:#89dceb;stroke-width:0.0678287;stroke-linecap:butt;stroke-linejoin:miter;stroke-dasharray:none;stroke-opacity:1"
                       d="m 72.80224,70.997602 c -5.502816,0.0409 -5.822744,-2.134625 -9.921011,-2.201202 h -0.0013 c -4.098214,0.06716 -4.418126,2.241098 -9.920959,2.201202 z" />
                  </g>
                </svg>
            </div>
        </nav>
    </header>

    {@render children()}
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

        svg {
            height: 8px;
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
            
            border: 2px solid #89dceb;
            border-top: none;

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

