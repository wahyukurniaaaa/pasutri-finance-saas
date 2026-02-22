<script lang="ts">
    import Card from "$lib/components/ui/Card.svelte";
</script>

<svelte:head>
    <title>Laporan - Finance Pasut</title>
</svelte:head>

<div class="p-6 pt-12 flex flex-col gap-6">
    <!-- Header -->
    <div class="flex justify-between items-center mb-4">
        <h1 class="text-2xl font-bold text-gray-900 flex items-center gap-2">
            📊 Laporan
        </h1>
        <select
            class="bg-slate-100 border-none rounded-lg px-3 py-1.5 text-sm font-medium text-gray-700 outline-none"
        >
            <option>Des 2024</option>
            <option>Nov 2024</option>
        </select>
    </div>

    <!-- Tabs -->
    <div class="flex p-1 bg-gray-100 rounded-xl">
        <button
            class="flex-1 py-1.5 rounded-lg font-medium text-sm transition-all text-gray-500 hover:bg-gray-200"
            >Harian</button
        >
        <button
            class="flex-1 py-1.5 rounded-lg font-medium text-sm transition-all text-gray-500 hover:bg-gray-200"
            >Mingguan</button
        >
        <button
            class="flex-1 py-1.5 rounded-lg font-medium text-sm transition-all bg-white shadow-sm text-gray-900"
            >Bulanan</button
        >
    </div>

    <!-- Pie Chart Placeholder -->
    <Card classProp="flex flex-col gap-4 relative overflow-hidden">
        <h3 class="font-bold text-gray-800">Pengeluaran per Kategori</h3>

        <div class="flex items-center gap-6 mt-4">
            <div
                class="w-32 h-32 rounded-full border-8 border-slate-100 relative shadow-inner"
            >
                <!-- CSS Pie Mockup -->
                <div
                    class="absolute inset-0 rounded-full border-[12px] border-emerald-500 border-t-transparent border-l-transparent transform rotate-45"
                ></div>
                <div
                    class="absolute inset-0 rounded-full border-[12px] border-amber-400 border-b-transparent border-r-transparent border-l-transparent transform rotate-[130deg]"
                ></div>
                <div
                    class="absolute inset-0 rounded-full border-[12px] border-rose-400 border-t-transparent border-r-transparent border-b-transparent transform rotate-[210deg]"
                ></div>
            </div>

            <div class="flex flex-col gap-3 flex-1">
                <div class="flex items-center justify-between text-xs">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-emerald-500"></div>
                        <span class="text-gray-600">Makan</span>
                    </div>
                    <span class="font-medium text-gray-900">35%</span>
                </div>
                <div class="flex items-center justify-between text-xs">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-amber-400"></div>
                        <span class="text-gray-600">Transport</span>
                    </div>
                    <span class="font-medium text-gray-900">20%</span>
                </div>
                <div class="flex items-center justify-between text-xs">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-rose-400"></div>
                        <span class="text-gray-600">Lainnya</span>
                    </div>
                    <span class="font-medium text-gray-900">45%</span>
                </div>
            </div>
        </div>
    </Card>

    <!-- Spender Insight -->
    <Card
        classProp="flex flex-col gap-4 bg-gradient-to-br from-indigo-50 to-purple-50"
    >
        <h3 class="font-bold text-gray-800 flex items-center gap-2">
            👫 Siapa Paling Boros?
        </h3>

        <div class="flex flex-col gap-5 mt-2">
            <!-- Suami -->
            <div class="flex flex-col gap-1">
                <div class="flex justify-between items-center text-sm">
                    <span class="flex items-center gap-2">👨 Suami</span>
                    <span class="font-bold text-gray-900">45%</span>
                </div>
                <div
                    class="w-full bg-indigo-100 h-2 rounded-full overflow-hidden"
                >
                    <div
                        class="w-[45%] bg-indigo-500 h-full rounded-full"
                    ></div>
                </div>
                <span class="text-xs text-gray-500 text-right"
                    >Rp 1.530.000</span
                >
            </div>

            <!-- Istri -->
            <div class="flex flex-col gap-1">
                <div class="flex justify-between items-center text-sm">
                    <span class="flex items-center gap-2">👩 Istri</span>
                    <span class="font-bold text-gray-900">55%</span>
                </div>
                <div
                    class="w-full bg-purple-100 h-2 rounded-full overflow-hidden"
                >
                    <div
                        class="w-[55%] bg-purple-500 h-full rounded-full"
                    ></div>
                </div>
                <span class="text-xs text-gray-500 text-right"
                    >Rp 1.870.000</span
                >
            </div>
        </div>
    </Card>

    <button
        class="w-full py-4 text-emerald-600 font-medium border border-emerald-200 rounded-xl bg-emerald-50 hover:bg-emerald-100 transition-colors mt-2"
    >
        📥 Export PDF
    </button>
</div>
