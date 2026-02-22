<script lang="ts">
    import Card from "$lib/components/ui/Card.svelte";
</script>

<svelte:head>
    <title>Goals - Finance Pasut</title>
</svelte:head>

<div class="p-6 pt-12 flex flex-col gap-6">
    <!-- Header -->
    <div class="flex justify-between items-center mb-2">
        <h1 class="text-2xl font-bold text-gray-900 flex items-center gap-2">
            🎯 Goals
        </h1>
        <button class="text-emerald-600 font-medium text-sm hover:underline"
            >+ Baru</button
        >
    </div>

    <div
        class="bg-emerald-600 text-white p-5 rounded-2xl shadow-lg shadow-emerald-500/20 flex flex-col gap-1"
    >
        <span class="text-emerald-100 text-sm">Total Tabungan Bersama</span>
        <span class="text-3xl font-bold">Rp 35.000.000</span>
    </div>

    <!-- Goals List -->
    <div class="flex flex-col gap-4 mt-2">
        <Card
            classProp="flex flex-col gap-4 border-emerald-100 hover:border-emerald-300 transition-colors"
        >
            <div class="flex items-center gap-3">
                <div
                    class="w-12 h-12 bg-sky-100 text-2xl flex items-center justify-center rounded-xl"
                >
                    🏖️
                </div>
                <div>
                    <h3 class="font-bold text-gray-900 text-lg">
                        Liburan Bali
                    </h3>
                    <p class="text-xs text-gray-500">
                        🎯 Target: Mar 2025 • ⏱️ 3 bln lagi
                    </p>
                </div>
            </div>

            <div>
                <div
                    class="flex justify-between text-xs font-medium text-gray-600 mb-1.5"
                >
                    <span>Rp 5.000.000</span>
                    <span>dari Rp 10.000.000</span>
                </div>
                <div
                    class="w-full bg-gray-100 h-2.5 rounded-full overflow-hidden"
                >
                    <div
                        class="w-[50%] bg-emerald-500 h-full rounded-full"
                    ></div>
                </div>
            </div>

            <button
                class="mt-2 w-full py-2.5 rounded-lg border-2 border-dashed border-gray-200 text-gray-600 font-medium text-sm hover:bg-gray-50 transition-colors"
            >
                + Tambah Dana
            </button>
        </Card>

        <Card
            classProp="flex flex-col gap-4 border-emerald-100 hover:border-emerald-300 transition-colors"
        >
            <div class="flex items-center gap-3">
                <div
                    class="w-12 h-12 bg-rose-100 text-2xl flex items-center justify-center rounded-xl"
                >
                    🏠
                </div>
                <div>
                    <h3 class="font-bold text-gray-900 text-lg">DP Rumah</h3>
                    <p class="text-xs text-gray-500">
                        🎯 Target: Des 2026 • ⏱️ 2 thn lagi
                    </p>
                </div>
            </div>

            <div>
                <div
                    class="flex justify-between text-xs font-medium text-gray-600 mb-1.5"
                >
                    <span>Rp 25.000.000</span>
                    <span>dari Rp 100.000.000</span>
                </div>
                <div
                    class="w-full bg-gray-100 h-2.5 rounded-full overflow-hidden"
                >
                    <div class="w-[25%] bg-amber-500 h-full rounded-full"></div>
                </div>
            </div>

            <button
                class="mt-2 w-full py-2.5 rounded-lg border-2 border-dashed border-gray-200 text-gray-600 font-medium text-sm hover:bg-gray-50 transition-colors"
            >
                + Tambah Dana
            </button>
        </Card>
    </div>
</div>
