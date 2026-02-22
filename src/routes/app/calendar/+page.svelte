<script lang="ts">
    import Card from "$lib/components/ui/Card.svelte";
</script>

<svelte:head>
    <title>Kalender Tagihan - Finance Pasut</title>
</svelte:head>

<div class="p-6 pt-12 flex flex-col gap-6">
    <!-- Header -->
    <div class="flex justify-between items-center mb-2">
        <h1 class="text-2xl font-bold text-gray-900 flex items-center gap-2">
            📅 Kalender
        </h1>
        <select class="bg-transparent font-semibold text-gray-700 outline-none">
            <option>Des 2024</option>
            <option>Nov 2024</option>
        </select>
    </div>

    <!-- Calendar Grid Mockup -->
    <div class="bg-white p-4 rounded-3xl border border-gray-100 shadow-sm">
        <div class="grid grid-cols-7 text-center mb-2">
            {#each ["S", "S", "R", "K", "J", "S", "M"] as day}
                <div class="text-[10px] font-bold text-gray-400 uppercase">
                    {day}
                </div>
            {/each}
        </div>
        <div class="grid grid-cols-7 text-center gap-y-2 text-sm">
            <!-- Empty start days -->
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            {#each Array(31) as _, i}
                <div
                    class="h-8 flex items-center justify-center relative {i +
                        1 ===
                    14
                        ? 'bg-emerald-500 text-white rounded-full font-bold shadow-md shadow-emerald-500/30'
                        : 'text-gray-700'}"
                >
                    {i + 1}
                    <!-- Events Mock -->
                    {#if i + 1 === 5}
                        <div class="absolute -bottom-1 text-[8px]">⚡</div>
                    {/if}
                    {#if i + 1 === 10}
                        <div class="absolute -bottom-1 text-[8px]">🏦</div>
                    {/if}
                </div>
            {/each}
        </div>
    </div>

    <div class="flex flex-col gap-3 mt-4">
        <h3 class="font-bold text-gray-800">Tagihan Bulan Ini</h3>

        <div
            class="flex items-center justify-between p-4 bg-white rounded-2xl border border-rose-100 shadow-sm relative overflow-hidden"
        >
            <div class="absolute left-0 top-0 bottom-0 w-1 bg-rose-500"></div>
            <div class="flex items-center gap-3">
                <div class="text-2xl">⚡</div>
                <div class="flex flex-col">
                    <span class="font-bold text-gray-900 leading-tight"
                        >Listrik PLN</span
                    >
                    <span class="text-xs text-rose-500 font-medium"
                        >Jatuh tempo: Tgl 5</span
                    >
                </div>
            </div>
            <div class="flex flex-col items-end gap-1">
                <span class="font-bold text-gray-900">Rp 450.000</span>
                <button
                    class="text-[10px] font-bold text-rose-600 bg-rose-50 px-2 py-1 rounded border border-rose-200 hover:bg-rose-100"
                >
                    TANDAI LUNAS
                </button>
            </div>
        </div>

        <div
            class="flex items-center justify-between p-4 bg-white rounded-2xl border border-gray-100 shadow-sm opacity-60"
        >
            <div class="absolute left-0 top-0 bottom-0 w-1 bg-gray-300"></div>
            <div class="flex items-center gap-3">
                <div class="text-2xl grayscale">🏦</div>
                <div class="flex flex-col">
                    <span
                        class="font-bold text-gray-900 leading-tight line-through"
                        >KPR Bank</span
                    >
                    <span class="text-xs text-gray-500">Tgl 10</span>
                </div>
            </div>
            <div class="flex flex-col items-end gap-1">
                <span class="font-bold text-gray-900 line-through"
                    >Rp 3.500.000</span
                >
                <span
                    class="text-[10px] font-bold text-emerald-600 flex items-center gap-1"
                >
                    ✓ LUNAS
                </span>
            </div>
        </div>

        <button
            class="w-full mt-2 py-3 rounded-xl border-2 border-dashed border-gray-200 text-gray-500 font-medium text-sm hover:bg-gray-50 hover:text-gray-700 transition-colors"
        >
            + Tambah Tagihan Rutin
        </button>
    </div>
</div>
