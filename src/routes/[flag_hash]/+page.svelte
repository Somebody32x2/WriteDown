<script lang="ts">
    // TODO: Page displaying grid of writeup solutions for the challenge with flag hash in url.
    // TODO: Fetch writeups from the server/load from server side.
    // Temp: sample writeup data
    import type { writeupInfo } from '$lib/flag_hash';
    import { onMount } from 'svelte';

    let location = '/writeup/';
    onMount(() => {
        if (window && window.location.href) {
            location = window.location.href;
        }
    });
    let sampleWriteupInfo: writeupInfo = {
        author: 'John Doe',
        date: '2021-10-10',
        content:
            'This is a writeup for the challenge. It contains the solution and explanation of the challenge.',
        path: 'john_doe_1'
    };
    let writeups: writeupInfo[] = [
        sampleWriteupInfo,
        sampleWriteupInfo,
        sampleWriteupInfo,
        sampleWriteupInfo,
        sampleWriteupInfo,
        sampleWriteupInfo
    ];
</script>

<div class="w-full bg-gray-800 min-h-screen flex flex-col items-center justify-center px-5">
    <div class="grid grid-cols-1 lg:grid-cols-2">
        {#each writeups as writeup}
            <div class="bg-gray-900 p-5 rounded-lg m-5">
                <h2 class="text-2xl text-white font-bold">{writeup.author}</h2>
                <p class="text-gray-400">{writeup.date}</p>
                <p class="text-gray-300">{writeup.content}</p>
                <a href={`${location}/${writeup.path}`} class="text-blue-500">Read more</a>
            </div>
        {/each}
    </div>
    <a
        href={location + '/create'}
        class="text-white m-10 text-xl font-bold bg-blue-900 p-3 rounded-lg border border-gray-500"
        >Create</a
    >
</div>
