<script lang="ts">
    import { media } from '$lib/api';
    import type { MovieListResult } from '$lib/types';

    export let movies: MovieListResult[];
    export let next: string | null;

    let viewport: HTMLDivElement;
    let results: HTMLDivElement;

    function handle_scroll() {}
</script>

<div bind:this={viewport} class="viewport" on:scroll={handle_scroll}>
    <div bind:this={results} class="results">
        {#each movies as movie}
            <a href="/movies/{movie.id}">
                <img alt={movie.title} src={media(movie.poster_path, 500)} />
            </a>
        {/each}
    </div>

    {#if next}
        <a href={next}>next page</a>
    {/if}
</div>

<style>
    .viewport {
        height: 500px;
        overflow-y: auto;
    }

    .results {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        width: 100%;
    }

    a {
        width: 100%;
        aspect-ratio: 2/3;
        height: auto;
        padding: 0.5rem;
    }

    img {
        width: 100%;
    }
</style>
