<script>
    // TODO: implement create page
    import SvelteMarkdown from 'svelte-markdown';
    import '$lib/restore_styling.css';
    import MarkdownEditor from './MarkdownEditor.svelte';

    let flag_text = 'flag{TODO_GET_FLAG_TEXT_TO_BE_HERE}';
    let source = `
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
| With two    | columns |`;
</script>

<div class="w-full bg-gray-800 min-h-screen flex flex-col items-center px-5">
    <h3 class="text-white text-2xl font-bold my-5">
        Creating Writeup for
        <div
            id="flag_preview"
            class="bg-white hover:bg-gray-700 transition-all duration-200 ease-in-out rounded-lg font-mono inline-block overflow-x-clip"
        >
            {flag_text}
        </div>
    </h3>
    <div
        class="flex w-full bg-gray-900 rounded-lg border border-gray-600 flex-grow my-5 overflow-hidden"
    >
        <div class="w-1/2 min-h-full border-r-2 border-r-gray-400 bg-gray-500 rounded-l-lg">
            <MarkdownEditor bind:text={source} />
        </div>
        <div
            class="restore_defaults text-white w-1/2 min-h-full pl-2 bg-gray-900 rounded-r-lg"
            id="markdown"
        >
            {#key source}
                <SvelteMarkdown {source} />
            {/key}
        </div>
    </div>
</div>

<style>
</style>
