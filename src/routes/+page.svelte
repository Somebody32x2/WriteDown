<script lang="ts">
    // TODO: (maybe server validation [must be a valid flag])
    async function handleFlagSubmit() {
        // Get and validate the flag
        const flagInput = document.getElementById('flagInput') as HTMLInputElement;
        const flag = flagInput.value.trim();
        if (!flag) {
            alert('Please enter a flag.');
            return;
        }
        // TODO: (possibly validate the flag contents are a real flag)
        // Hash the flag using sha256 subtle crypto
        const encoder = new TextEncoder();
        const data = encoder.encode(flag);
        const hash = await crypto.subtle.digest('SHA-256', data);
        // Convert the hash to a hex string
        const hashArray = Array.from(new Uint8Array(hash));
        const hashHex = hashArray.map((b) => b.toString(16).padStart(2, '0')).join('');
        if (window && window.location) {
            window.location.href = `/${hashHex}`;
        }
    }
</script>

<div class="w-full bg-gray-800 min-h-screen flex flex-col items-center justify-center px-5">
    <div class="pb-10 flex flex-col items-center text-white">
        <h1 class="text-white text-4xl font-black">WriteDown</h1>
        <h4 class="text-lg font-bold">The CTF Writeup Sharing Solution</h4>
    </div>
    <div
        class="flex flex-col items-center justify-center border-gray-500 bg-gray-700 border rounded-2xl h-[80vh] w-full md:w-7/12"
    >
        <label for="flagInput" class="text-2xl text-center text-white font-bold mb-10"
            >Enter Your Flag:</label
        >
        <input
            id="flagInput"
            class="bg-gray-900 w-[20rem] border-gray-500 border-2 rounded text-white font-mono"
            maxlength="100"
            type="text"
            placeholder="prefix{`{__FLAG__}`}"
        />
        <button
            on:click={handleFlagSubmit}
            class="text-white m-10 text-xl font-bold bg-blue-900 p-3 rounded-lg border border-gray-500"
            >Go!</button
        >
        <p
            id="message-not-found-error"
            class="text-xl font-bold text-red-600 mt-10 text-center hidden"
        >
            The Requested Flag was Not Found.
        </p>
        <p
            id="message-general-error"
            class="text-xl font-bold text-red-600 mt-10 text-center hidden"
        >
            An Error Occurred.<br />Please try again and report to your CTF organizer if the error
            persists.
        </p>
    </div>
</div>
