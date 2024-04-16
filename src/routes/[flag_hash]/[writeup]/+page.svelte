<script lang="ts">
    // Temp: sample writeup data
    import type { writeupInfo } from '$lib/flag_hash';
    import SvelteMarkdown from 'svelte-markdown';
    import '$lib/restore_styling.css';

    let sampleWriteupInfo: writeupInfo = {
        author: 'John Doe',
        date: '2021-10-10',
        content: `
# This is a Header
## This is a subheader
### This is a subsubheader
This is a paragraph.

* This is a list
* With two items
  1. And a sublist
  2. That is ordered
    * With another
    * Sublist inside

| And this is | A table |
|-------------|---------|
| With two    | columns |`,
        path: 'john_doe_1'
    };
    let writeup: writeupInfo = sampleWriteupInfo;
</script>

<div class="w-full text-white bg-gray-800 min-h-screen flex flex-col items-center p-5">
    <h1 class="text-3xl font-bold">{writeup.author}</h1>
    <p>{writeup.date}</p>
    <!--    TODO: Add Markdown Rendering Library Here-->
    <div
        class="bg-gray-900 w-full lg:w-2/3 flex-grow mt-5 rounded-lg border border-gray-600 overflow-hidden"
    >
        <div
            class="restore_defaults text-white w-1/2 min-h-full pl-2 bg-gray-900 rounded-r-lg"
            id="markdown"
        >
            <SvelteMarkdown source={writeup.content} />
        </div>
    </div>
</div>
