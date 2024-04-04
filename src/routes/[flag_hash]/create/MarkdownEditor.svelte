<script lang="ts">
    export let text: string = '';

    function applyMarkdownModifier(symbol: string) {
        return () => {
            const textarea = document.getElementById('editor_textarea') as HTMLTextAreaElement;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;
            const selectedText = textarea.value.substring(start, end);
            const expandedSelectedText = textarea.value.substring(
                start - symbol.length,
                end + symbol.length
            );
            // Check if the selected text is already immediately wrapped in the symbol
            // TODO: Handle bold/italic text that is partially or double wrapped in the symbol
            if (expandedSelectedText.startsWith(symbol) && expandedSelectedText.endsWith(symbol)) {
                const newText =
                    textarea.value.substring(0, start - symbol.length) +
                    selectedText +
                    textarea.value.substring(end + symbol.length);
                textarea.value = newText;
                textarea.focus();
                textarea.setSelectionRange(start - symbol.length, end - symbol.length);
                text = textarea.value;
                return;
            }
            // TODO: Fix/Remove removal of already selected modifiers when toggling that one
            if (selectedText.startsWith(symbol) && selectedText.endsWith(symbol)) {
                const replacement = selectedText.substring(
                    symbol.length,
                    selectedText.length - symbol.length
                );
                textarea.value =
                    textarea.value.substring(0, start) +
                    replacement +
                    textarea.value.substring(end);
                textarea.focus();
                textarea.setSelectionRange(start, end - symbol.length);
                text = textarea.value;
                return;
            }
            const replacement = `${symbol}${selectedText}${symbol}`;
            textarea.value =
                textarea.value.substring(0, start) + replacement + textarea.value.substring(end);
            textarea.focus();
            textarea.setSelectionRange(start + symbol.length, end + symbol.length);
            text = textarea.value;
        };
    }
</script>

<div class="w-full h-full flex flex-col">
    <!--    Controls-->
    <div class="w-full h-8 bg-gray-600">
        <!--        TODO: FINISH CONTROL STYLING & ADD ICONS-->
        <button
            on:click={applyMarkdownModifier('**')}
            class="text-white w-8 border border-gray-500 h-full ml-2 rounded-lg px-2 font-bold bg-blue-900 ring-gray-500 active:ring-4"
            >B</button
        >
        <button
            on:click={applyMarkdownModifier('*')}
            class="text-white italic w-8 border border-gray-500 h-full rounded-lg px-2 font-bold bg-blue-900 ring-gray-500 active:ring-4"
            >I
        </button>
        <button
            on:click={applyMarkdownModifier('`')}
            class="text-white border w-12 border-gray-500 h-full rounded-lg px-2 font-bold bg-blue-900 ring-gray-500 active:ring-4"
            >{`</>`}
        </button>
        <button
            on:click={applyMarkdownModifier('~~')}
            class="text-white w-8 line-through border border-gray-500 h-full rounded-lg px-2 font-bold bg-blue-900 ring-gray-500 active:ring-4"
            >S
        </button>
    </div>
    <div class="w-full h-full">
        <textarea
            id="editor_textarea"
            class="form-control w-full min-h-full bg-gray-900 resize-none text-white pl-1 outline-none"
            rows="5"
            bind:value={text}
        ></textarea>
    </div>
</div>
