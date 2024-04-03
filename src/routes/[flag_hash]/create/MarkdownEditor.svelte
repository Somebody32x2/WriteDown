<script lang="ts">
    export let text: string = '';
</script>

<div class="w-full h-full flex flex-col">
    <!--    Controls-->
    <div class="w-full h-8 bg-gray-600">
        <!--        TODO: FINISH CONTROL STYLING & ADD ICONS + FUNCTIONALITY-->
        <button
            class="text-white border border-gray-500 h-full ml-2 rounded-lg px-2 font-bold bg-blue-900 ring-gray-500 active:ring-4"
            >H1</button
        >
    </div>
    <div class="w-full h-full">
        <textarea
            class="form-control w-full min-h-full bg-gray-900 resize-none text-white"
            rows="5"
            bind:value={text}
        ></textarea>
    </div>
</div>
