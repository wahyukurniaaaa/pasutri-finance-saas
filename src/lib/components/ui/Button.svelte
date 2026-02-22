<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let type: "button" | "submit" | "reset" = "button";
    export let variant: "primary" | "secondary" | "outline" | "ghost" =
        "primary";
    export let size: "sm" | "md" | "lg" = "md";
    export let disabled = false;
    export let fullWidth = false;
    export let classProp = "";

    const dispatch = createEventDispatcher();

    const baseClasses =
        "inline-flex items-center justify-center font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 disabled:opacity-50 disabled:pointer-events-none rounded-lg";

    const variants = {
        primary:
            "bg-emerald-600 text-white hover:bg-emerald-700 focus:ring-emerald-500",
        secondary:
            "bg-gray-100 text-gray-900 hover:bg-gray-200 focus:ring-gray-500",
        outline:
            "border border-gray-300 bg-transparent text-gray-700 hover:bg-gray-50 focus:ring-emerald-500",
        ghost: "bg-transparent text-gray-700 hover:bg-gray-100 focus:ring-gray-500",
    };

    const sizes = {
        sm: "h-9 px-3 text-sm",
        md: "h-11 px-6 text-base",
        lg: "h-14 px-8 text-lg",
    };
</script>

<button
    {type}
    {disabled}
    on:click={(e) => dispatch("click", e)}
    class="{baseClasses} {variants[variant]} {sizes[size]} {fullWidth
        ? 'w-full'
        : ''} {classProp}"
    {...$$restProps}
>
    <slot />
</button>
