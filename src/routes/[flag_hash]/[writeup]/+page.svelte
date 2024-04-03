<script lang="ts">
    // Temp: sample writeup data
    import type { writeupInfo } from '$lib/flag_hash';

    let sampleWriteupInfo: writeupInfo = {
        author: 'John Doe',
        date: '2021-10-10',
        content:
            'This is a writeup for the challenge. It contains the solution and explanation of the challenge.',
        path: 'john_doe_1'
    };
    let writeup: writeupInfo = sampleWriteupInfo;
</script>

<div class="w-full text-white bg-gray-800 min-h-screen flex flex-col items-center p-5">
    <h1 class="text-3xl font-bold">{writeup.author}</h1>
    <p>{writeup.date}</p>
    <!--    TODO: Add Markdown Rendering Library Here-->
    <div
        class="bg-gray-900 font-mono w-full lg:w-2/3 flex-grow mt-5 rounded-lg border border-gray-600"
    >
        <p>{writeup.content}</p>
    </div>
</div>
