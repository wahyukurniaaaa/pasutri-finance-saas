<script lang="ts">
    export let classProp = "";
    export let glass = false; // glassmorphism effect
</script>

<div
    class={`rounded-xl border border-gray-200 bg-white p-6 shadow-sm ${glass ? "bg-white/70 backdrop-blur-md border-white/50" : ""} ${classProp}`}
    {...$$restProps}
>
    <slot />
</div>
