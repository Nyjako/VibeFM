<script lang="ts">
    import PlayePauseButton from "./PlayePauseButton.svelte";

    let song_title = "Test title"
    let song_artist = "Test author"

    let player_height = "80px"

</script>

<div class="player-container" style="--player-height: {player_height}">
    <div class="spacer-left"></div>

    <div class="play-pause-button">
        <PlayePauseButton 
            fill_color="rgb(33, 33, 33)"
            background_color="rgb(230, 230, 230)"
            background_size={50}
            button_width={20}
        />
    </div>

    <div class="song-details">
        <p class="title" >{song_title}</p>
        <p>By <span class="artist">{song_artist}</span></p>
    </div>

    <div class="spacer-right"></div>
</div>

<style>
    .player-container {
        width: 100vw;
        height: var(--player-height);
        display: flex;
        align-items: center;
        gap: 25px;
        background-color: rgb(33, 33, 33);
    }

    .song-details {
        flex-grow: 1;
    }

    .song-details > p {
        margin: 0;
    }

    .title {
        font-family: 'Roboto Black', sans-serif;
        font-size: x-large;
        font-weight: bolder;
    }

    .artist {
        font-family: 'Roboto Black', sans-serif;
        font-size: medium;
        font-weight: bold;
    }

    .play-pause-button {
        flex-shrink: 1;
    }

    .spacer-left, .spacer-right {
        width: 50px;
        height: var(--player-height);
        flex-shrink: 1;
        opacity: 0.3;
    }

    .spacer-left { background: linear-gradient(to right, black, transparent); }
    .spacer-right { background: linear-gradient(to left, black, transparent); }


</style>