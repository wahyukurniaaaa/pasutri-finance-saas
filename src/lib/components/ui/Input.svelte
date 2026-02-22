<script lang="ts">
    export let type = "text";
    export let value = "";
    export let placeholder = "";
    export let label = "";
    export let error = "";
    export let id = Math.random().toString(36).substring(2, 9);
    export let disabled = false;
    export let classProp = "";
    export let iconClass = ""; // optional icon or emoji wrapper

    // For password toggle
    let showPassword = false;
    $: currentType = type === "password" && showPassword ? "text" : type;
</script>

<div class={`w-full flex flex-col gap-1.5 ${classProp}`}>
    {#if label}
        <label for={id} class="text-xs font-medium text-gray-600">{label}</label
        >
    {/if}
    <div class="relative">
        {#if iconClass}
            <div
                class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-gray-500"
            >
                <span class={iconClass}></span>
            </div>
        {/if}
        <input
            {id}
            type={currentType}
            bind:value
            {placeholder}
            {disabled}
            class="flex h-12 w-full rounded-lg border border-gray-300 bg-white px-3 py-2 text-sm placeholder:text-gray-400 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 disabled:cursor-not-allowed disabled:opacity-50 {iconClass
                ? 'pl-9'
                : ''} {error ? 'border-red-500 focus:ring-red-500' : ''}"
            {...$$restProps}
            on:input
            on:blur
        />
        {#if type === "password"}
            <button
                type="button"
                class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-500 hover:text-gray-700"
                on:click={() => (showPassword = !showPassword)}
            >
                {showPassword ? "👁️‍🗨️" : "👁️"}
            </button>
        {/if}
    </div>
    {#if error}
        <p class="text-xs text-red-500">{error}</p>
    {/if}
</div>
