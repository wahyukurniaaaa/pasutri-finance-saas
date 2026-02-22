<script lang="ts">
    import Card from "$lib/components/ui/Card.svelte";

    // Fake data for UI prototype
    const user = { name: "Wahyu", role: "Suami" };

    const budget = {
        total: 5000000,
        used: 3450000,
    };

    $: budgetRemaining = budget.total - budget.used;
    $: budgetPercent = Math.round((budget.used / budget.total) * 100);

    const stats = {
        income: { amount: 8500000, trend: 12, isUp: true },
        expense: { amount: 4200000, trend: 5, isUp: false },
    };

    const transactions = [
        {
            id: 1,
            title: "Makan Siang",
            amount: -50000,
            category: "🍜",
            who: "Istri",
            time: "2 jam lalu",
        },
        {
            id: 2,
            title: "Bensin",
            amount: -100000,
            category: "⛽",
            who: "Suami",
            time: "5 jam lalu",
        },
        {
            id: 3,
            title: "Groceries",
            amount: -350000,
            category: "🛒",
            who: "Istri",
            time: "Kemarin",
        },
    ];

    function formatCurrency(amount: number) {
        return new Intl.NumberFormat("id-ID", {
            style: "currency",
            currency: "IDR",
            maximumFractionDigits: 0,
        }).format(amount);
    }

    function formatShortCurrency(amount: number) {
        if (amount >= 1000000) return (amount / 1000000).toFixed(1) + " jt";
        if (amount >= 1000) return (amount / 1000).toFixed(0) + " rb";
        return amount.toString();
    }
</script>

<svelte:head>
    <title>Dashboard - Finance Pasut</title>
</svelte:head>

<div class="p-6 pt-12 flex flex-col gap-8 pb-32">
    <!-- Header -->
    <div
        class="flex justify-between items-center bg-white/50 backdrop-blur-md p-4 rounded-2xl sticky top-4 z-40 border border-white/40 shadow-sm"
    >
        <div class="flex items-center gap-3">
            <div
                class="w-10 h-10 rounded-full bg-emerald-100 flex items-center justify-center text-xl"
            >
                {user.role === "Suami" ? "👨" : "👩"}
            </div>
            <div>
                <p class="text-sm text-gray-500">Hai,</p>
                <p class="font-bold text-gray-900">{user.name}</p>
            </div>
        </div>
        <div class="flex gap-3 text-2xl text-gray-600">
            <button
                class="relative hover:bg-gray-100 p-2 rounded-full transition-colors"
            >
                🔔
                <span
                    class="absolute top-2 right-2 w-2.5 h-2.5 bg-red-500 border-2 border-white rounded-full"
                ></span>
            </button>
            <button class="hover:bg-gray-100 p-2 rounded-full transition-colors"
                >⚙️</button
            >
        </div>
    </div>

    <!-- Summary Card -->
    <div
        class="relative overflow-hidden rounded-3xl bg-gradient-to-br from-emerald-600 to-teal-800 p-6 text-white shadow-xl shadow-emerald-500/20"
    >
        <div
            class="absolute top-0 right-0 -m-8 w-32 h-32 bg-white opacity-10 rounded-full blur-2xl"
        ></div>
        <div
            class="absolute bottom-0 left-0 -m-8 w-40 h-40 bg-emerald-400 opacity-20 rounded-full blur-3xl"
        ></div>

        <div class="relative z-10 flex flex-col gap-6">
            <div class="flex flex-col gap-1 text-emerald-50">
                <h2 class="text-sm font-medium opacity-90">
                    Sisa Anggaran Bulan Ini
                </h2>
                <p class="text-4xl font-bold tracking-tight">
                    {formatCurrency(budgetRemaining)}
                </p>
            </div>

            <div class="flex flex-col gap-2">
                <div
                    class="flex justify-between text-xs font-medium text-emerald-100"
                >
                    <span>Terpakai {budgetPercent}%</span>
                    <span>dari {formatCurrency(budget.total)}</span>
                </div>
                <div
                    class="w-full h-2 bg-emerald-900/50 rounded-full overflow-hidden"
                >
                    <div
                        class="h-full bg-gradient-to-r from-emerald-300 to-white rounded-full transition-all duration-1000 ease-out shadow-[0_0_10px_rgba(255,255,255,0.5)]"
                        style="width: {budgetPercent}%"
                    ></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Quick Stats -->
    <div class="grid grid-cols-2 gap-4">
        <Card
            classProp="flex flex-col gap-2 p-5 !border-none !shadow-md shadow-gray-200/50 relative overflow-hidden"
        >
            <div
                class="absolute -right-4 -bottom-4 text-6xl opacity-5 grayscale"
            >
                💰
            </div>
            <div
                class="flex items-center gap-2 text-gray-500 font-medium text-sm"
            >
                <span
                    class="bg-emerald-100 text-emerald-600 p-1.5 rounded-lg text-xs"
                    >💰</span
                > Income
            </div>
            <p class="text-2xl font-bold text-gray-900">
                +{formatShortCurrency(stats.income.amount)}
            </p>
            <div
                class="text-xs font-semibold flex items-center gap-1 {stats
                    .income.isUp
                    ? 'text-emerald-500'
                    : 'text-red-500'} bg-emerald-50 w-fit px-2 py-1 rounded-md"
            >
                {stats.income.isUp ? "▲" : "▼"}
                {stats.income.trend}%
            </div>
        </Card>

        <Card
            classProp="flex flex-col gap-2 p-5 !border-none !shadow-md shadow-gray-200/50 relative overflow-hidden"
        >
            <div
                class="absolute -right-4 -bottom-4 text-6xl opacity-5 grayscale"
            >
                💸
            </div>
            <div
                class="flex items-center gap-2 text-gray-500 font-medium text-sm"
            >
                <span class="bg-rose-100 text-rose-600 p-1.5 rounded-lg text-xs"
                    >💸</span
                > Expense
            </div>
            <p class="text-2xl font-bold text-gray-900">
                -{formatShortCurrency(stats.expense.amount)}
            </p>
            <div
                class="text-xs font-semibold flex items-center gap-1 {stats
                    .expense.isUp
                    ? 'text-emerald-500'
                    : 'text-red-500'} bg-rose-50 w-fit px-2 py-1 rounded-md"
            >
                {stats.expense.isUp ? "▲" : "▼"}
                {stats.expense.trend}%
            </div>
        </Card>
    </div>

    <!-- Recent Transactions -->
    <div class="flex flex-col gap-4">
        <div class="flex justify-between items-end mb-2">
            <h3 class="text-lg font-bold text-gray-900">Transaksi Terakhir</h3>
            <a
                href="/app/transactions"
                class="text-sm font-medium text-emerald-600 hover:text-emerald-700 hover:underline"
                >Semua &gt;</a
            >
        </div>

        <div class="flex flex-col gap-3">
            {#each transactions as trx (trx.id)}
                <div
                    class="bg-white p-4 rounded-2xl flex items-center justify-between border border-gray-100 shadow-sm hover:border-emerald-200 transition-colors group cursor-pointer"
                >
                    <div class="flex items-center gap-4">
                        <div
                            class="w-12 h-12 bg-slate-100 rounded-xl flex items-center justify-center text-2xl group-hover:bg-emerald-50 transition-colors"
                        >
                            {trx.category}
                        </div>
                        <div class="flex flex-col">
                            <span class="font-semibold text-gray-900"
                                >{trx.title}</span
                            >
                            <span
                                class="text-xs text-gray-500 flex items-center gap-1 mt-0.5"
                            >
                                <span class="font-medium text-gray-700"
                                    >{trx.who}</span
                                >
                                • {trx.time}
                            </span>
                        </div>
                    </div>
                    <div class="font-bold text-gray-900 whitespace-nowrap">
                        {new Intl.NumberFormat("id-ID").format(trx.amount)}
                    </div>
                </div>
            {/each}
        </div>
    </div>
</div>
