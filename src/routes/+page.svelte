<script lang="ts">
    import { invoke } from "@tauri-apps/api/core";
    import AudioPlayer from "../lib/AudioPlayer.svelte";

    let name = "";
    let greetMsg = "";

    async function greet() {
      // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
        greetMsg = await invoke("greet", { name });
    }
</script>

<div class="container">
    <AudioPlayer stream=""/>
</div>

<style>
    :global(body) {
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0;
        padding: 0;
    }

    :root {
        color: #0f0f0f;
        background-color: #f6f6f6;
        margin: 0;
        padding: 0;

        font-synthesis: none;
        text-rendering: optimizeLegibility;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        -webkit-text-size-adjust: 100%;
    }

    @media (prefers-color-scheme: dark) {
        :root {
            color: #f6f6f6;
            background-color: #2f2f2f;
        }
    }
</style>
