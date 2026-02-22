<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";

    let type: "expense" | "income" = "expense";
    let amountStr = "";
    let selectedCategory = "";
    let selectedWallet = "istri";
    let notes = "";

    const categories = {
        expense: [
            { id: "food", icon: "🍜", label: "Makan" },
            { id: "transport", icon: "🚗", label: "Trnsprt" },
            { id: "home", icon: "🏠", label: "Rumah" },
            { id: "shop", icon: "🛒", label: "Belanja" },
            { id: "util", icon: "⚡", label: "Listrik" },
            { id: "kids", icon: "👶", label: "Anak" },
            { id: "ent", icon: "🎬", label: "Hiburan" },
            { id: "health", icon: "🏥", label: "Sehat" },
        ],
        income: [
            { id: "salary", icon: "💼", label: "Gaji" },
            { id: "bonus", icon: "💵", label: "Bonus" },
            { id: "invest", icon: "📈", label: "Invest" },
            { id: "gift", icon: "🎁", label: "Hadiah" },
        ],
    };

    const wallets = [
        { id: "suami", label: "Suami" },
        { id: "istri", label: "Istri" },
        { id: "joint", label: "Rekening Bersama" },
    ];

    function handleNumpad(key: string) {
        if (key === "BACK") {
            amountStr = amountStr.slice(0, -1);
        } else if (key === "000") {
            if (amountStr.length > 0) amountStr += "000";
        } else {
            // prevent leading zeros if not decimal (simplified)
            if (amountStr === "" && key === "0") return;
            amountStr += key;
        }
    }

    $: displayAmount = amountStr
        ? new Intl.NumberFormat("id-ID").format(parseInt(amountStr))
        : "0";
    $: isValid =
        amountStr.length > 0 &&
        parseInt(amountStr) > 0 &&
        selectedCategory !== "";

    function handleSubmit() {
        window.location.href = "/app/dashboard";
    }
</script>

<svelte:head>
    <title>Tambah Transaksi - Finance Pasut</title>
</svelte:head>

<div class="fixed inset-0 bg-slate-50 z-50 flex flex-col pt-safe px-4 pt-12">
    <!-- Header -->
    <div class="flex justify-between items-center mb-6 px-2">
        <h1 class="text-xl font-bold text-gray-900">Tambah Transaksi</h1>
        <a
            href="javascript:history.back()"
            class="w-8 h-8 flex items-center justify-center rounded-full bg-gray-100 text-gray-500 hover:bg-gray-200"
        >
            ✕
        </a>
    </div>

    <!-- Type Toggle -->
    <div class="flex p-1 bg-gray-100 rounded-xl mb-8">
        <button
            class="flex-1 py-2.5 rounded-lg font-medium text-sm transition-all flex items-center justify-center gap-2 {type ===
            'expense'
                ? 'bg-white shadow-sm text-rose-600'
                : 'text-gray-500 hover:bg-gray-200/50'}"
            on:click={() => {
                type = "expense";
                selectedCategory = "";
            }}
        >
            <span>💸</span> Pengeluaran
        </button>
        <button
            class="flex-1 py-2.5 rounded-lg font-medium text-sm transition-all flex items-center justify-center gap-2 {type ===
            'income'
                ? 'bg-white shadow-sm text-emerald-600'
                : 'text-gray-500 hover:bg-gray-200/50'}"
            on:click={() => {
                type = "income";
                selectedCategory = "";
            }}
        >
            <span>💰</span> Pemasukan
        </button>
    </div>

    <!-- Amount Display -->
    <div class="flex justify-center mb-8">
        <div class="text-center">
            <span class="text-2xl font-bold text-gray-400 mr-1 opacity-50"
                >Rp</span
            >
            <span
                class="text-5xl font-bold tracking-tight text-gray-900 {type ===
                'expense'
                    ? ''
                    : 'text-emerald-500'}"
            >
                {displayAmount}
            </span>
        </div>
    </div>

    <div class="flex-1 overflow-y-auto no-scrollbar pb-6 flex flex-col gap-8">
        <!-- Categories -->
        <div class="grid grid-cols-4 gap-3">
            {#each categories[type] as cat (cat.id)}
                <button
                    class="flex flex-col items-center justify-center gap-2 p-3 rounded-2xl border-2 transition-all {selectedCategory ===
                    cat.id
                        ? type === 'expense'
                            ? 'border-rose-500 bg-rose-50 ring-2 ring-rose-100'
                            : 'border-emerald-500 bg-emerald-50 ring-2 ring-emerald-100'
                        : 'border-gray-100 bg-white hover:border-gray-200 hover:bg-gray-50/50'}"
                    on:click={() => (selectedCategory = cat.id)}
                >
                    <span class="text-3xl filter drop-shadow-sm"
                        >{cat.icon}</span
                    >
                    <span
                        class="text-[10px] font-medium text-gray-600 truncate w-full text-center"
                        >{cat.label}</span
                    >
                </button>
            {/each}
        </div>

        <!-- Source Wallet -->
        <div class="flex flex-col gap-3">
            <label class="text-sm font-semibold text-gray-700"
                >Sumber Dana</label
            >
            <div class="flex flex-wrap gap-2">
                {#each wallets as wallet (wallet.id)}
                    <button
                        class="px-4 py-2.5 rounded-xl text-sm font-medium border transition-colors flex items-center gap-2 {selectedWallet ===
                        wallet.id
                            ? 'border-emerald-500 bg-emerald-50 py-2.5 text-emerald-700'
                            : 'border-gray-200 bg-white text-gray-600 hover:bg-slate-50'}"
                        on:click={() => (selectedWallet = wallet.id)}
                    >
                        <div
                            class="w-3.5 h-3.5 rounded-full border-2 flex items-center justify-center {selectedWallet ===
                            wallet.id
                                ? 'border-emerald-500 bg-emerald-500'
                                : 'border-gray-300'}"
                        ></div>
                        {wallet.label}
                    </button>
                {/each}
            </div>
        </div>

        <!-- Notes -->
        <div class="flex flex-col gap-2">
            <label class="text-sm font-semibold text-gray-700"
                >Catatan (opsional)</label
            >
            <input
                type="text"
                bind:value={notes}
                placeholder="Makan siang dengan klien..."
                class="w-full h-12 bg-white border border-gray-200 rounded-xl px-4 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500"
            />
        </div>

        <div class="mt-4">
            <Button
                fullWidth
                size="lg"
                on:click={handleSubmit}
                disabled={!isValid}
                classProp={type === "expense" && isValid
                    ? "bg-rose-600 hover:bg-rose-700 focus:ring-rose-500"
                    : ""}
            >
                SIMPAN TRANSAKSI
            </Button>
        </div>
    </div>

    <!-- Numpad (Fixed Bottom) -->
    <div
        class="mt-auto pt-4 pb-8 border-t border-gray-100 bg-white/80 backdrop-blur-xl -mx-4 px-4"
    >
        <div class="grid grid-cols-3 gap-2 max-w-sm mx-auto">
            {#each ["1", "2", "3", "4", "5", "6", "7", "8", "9", "000", "0", "BACK"] as key}
                <button
                    class="h-14 rounded-xl flex items-center justify-center text-2xl font-semibold transition-colors active:scale-95 {key ===
                    'BACK'
                        ? 'text-rose-500 bg-rose-50 hover:bg-rose-100'
                        : 'text-gray-800 bg-white border border-gray-100 hover:bg-gray-50 shadow-sm'}"
                    on:click={() => handleNumpad(key)}
                >
                    {#if key === "BACK"}
                        ⌫
                    {:else}
                        {key}
                    {/if}
                </button>
            {/each}
        </div>
    </div>
</div>
