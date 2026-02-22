<script lang="ts">
    import { page } from "$app/stores";

    const userRoleStr = "👨"; // Mocked

    const navItems = [
        { name: "Home", icon: "🏠", path: "/app/dashboard" },
        { name: "Report", icon: "📊", path: "/app/reports" },
        { name: "Add", icon: "➕", path: "/app/transaction/new", isFab: true },
        { name: "Goals", icon: "🎯", path: "/app/goals" },
        { name: "Me", icon: userRoleStr, path: "/app/profile" },
    ];
</script>

<nav
    class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-100 px-6 py-2 pb-safe shadow-[0_-4px_20px_-10px_rgba(0,0,0,0.05)] z-50 rounded-t-2xl"
>
    <ul class="flex justify-between items-center max-w-md mx-auto">
        {#each navItems as item}
            <li class="relative">
                <a
                    href={item.path}
                    class="flex flex-col items-center justify-center gap-1 w-14 {item.isFab
                        ? '-translate-y-5'
                        : ''}"
                >
                    {#if item.isFab}
                        <div
                            class="w-14 h-14 bg-emerald-500 rounded-full flex items-center justify-center text-white text-2xl shadow-lg shadow-emerald-500/30 hover:bg-emerald-600 transition-colors border-4 border-white"
                        >
                            {item.icon}
                        </div>
                    {:else}
                        {@const isActive = $page.url.pathname === item.path}
                        <div
                            class="text-2xl transition-all duration-300 {isActive
                                ? 'scale-110 -translate-y-1 drop-shadow-sm brightness-110'
                                : 'opacity-60 grayscale hover:grayscale-0'}"
                        >
                            {item.icon}
                        </div>
                        <span
                            class="text-[10px] font-medium transition-colors {isActive
                                ? 'text-emerald-600'
                                : 'text-gray-400'}"
                        >
                            {item.name}
                        </span>
                        {#if isActive}
                            <div
                                class="absolute -bottom-2 w-1 h-1 rounded-full bg-emerald-500"
                            ></div>
                        {/if}
                    {/if}
                </a>
            </li>
        {/each}
    </ul>
</nav>

<div class="pb-24">
    <slot />
</div>
