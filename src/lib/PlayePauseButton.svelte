<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import { tweened } from 'svelte/motion';
    import { cubicInOut } from 'svelte/easing';

    export let background_color: String = "#eee";
    export let fill_color: String = "#4d4d4d";
    export let background_size: number = 70;
    export let button_width: number = 33;

    const pausePaths = [
      'M212.13203,347.27573L280.82241,347.27573L280.82241,627.08798L212.13203,627.08798Z',
      'M393.9595,347.27573L462.64988,347.27573L462.64988,627.08798L393.9595,627.08798Z',
    ];
    const playPaths = [
      'M246.84631,381.58161L341.39093,434.38173L341.39093,539.98196L246.84631,592.7821Z',
      'M341.39093,434.38173L435.22131,487.18188L435.22131,487.18188L341.39093,539.98195Z',
    ];
  
    const pauseCoords = pathsToCoords(pausePaths);
    const playCoords = pathsToCoords(playPaths);
  
    const progress = tweened(pauseCoords, {
        duration: 400,
        easing: cubicInOut,
    });
  
    let isPlaying = true;
    const dispatch = createEventDispatcher();
    dispatch("buttonState", {isPlaying}); // just to make sure everything is setup correctly

    function onToggle() {
        isPlaying ? progress.set(playCoords) : progress.set(pauseCoords);
        isPlaying = !isPlaying;
        dispatch("buttonState", {isPlaying});
    }
  
    function pathsToCoords(paths: String[]): number[][] {
        return paths.map((d) =>
            d
                .replace(/[LMZ]/g, ',')
                .split(',')
                .filter(String)
                .map((c) => Number(c))
        );
    }
  
    function coordsToPath(coords: number[]) {
        const joinedInstructions = coords.reduce((acc, cur, i) => (i % 2 !== 0 ? acc + cur + 'L' : acc + cur + ','), '');
        return `M${joinedInstructions}Z`;
    }
</script>
  
<main>
    <button 
        class="button-background"
        style="--background_color: {background_color}; --fill_color: {fill_color}; --background_size: {background_size}px"
        on:click={onToggle}
    >
        <svg 
            xmlns="http://www.w3.org/2000/svg" 
            viewBox="0 0 250.51786 279.81226" 
            width={button_width}
        >
            <g transform="translate(-212.13203,-347.27573)">
            <path d={coordsToPath($progress[0])} />
            <path d={coordsToPath($progress[1])} />
            </g>
        </svg>
    </button>
</main>
  
<style>
    .button-background {
        width: var(--background_size);
        height: var(--background_size);
        border: none;
        border-radius: 50%;
        background-color: var(--background_color);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    button:active:focus, button:focus {
        outline: none;
        box-shadow: none;
        background-color: var(--background_color);
    }

    .button-background:hover {
        cursor: pointer;
    }

    path {
        opacity: 1;
        fill: var(--fill_color);
        fill-opacity: 1;
        stroke: var(--fill_color);
        stroke-width: 7;
    }
</style>
