<script lang="ts">
    import BottomNav from "$lib/components/ui/BottomNav.svelte";
</script>

<div class="h-full bg-slate-50 min-h-screen">
    <slot />
    <BottomNav />
</div>
