<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";
    import Input from "$lib/components/ui/Input.svelte";

    // For initial setup logic
    let wallets = [
        { id: 1, name: "Kas Tunai", amount: "" },
        { id: 2, name: "Rekening Bank", amount: "" },
        { id: 3, name: "E-Wallet (GoPay/OVO/dll)", amount: "" },
    ];

    function addWallet() {
        wallets = [
            ...wallets,
            { id: Date.now(), name: "Dompet Baru", amount: "" },
        ];
    }

    function removeWallet(id: number) {
        wallets = wallets.filter((w) => w.id !== id);
    }

    // Format currency helper
    function formatCurrency(val: string) {
        // simple formatter for UI prototype
        const num = val.replace(/\D/g, "");
        return num ? parseInt(num).toLocaleString("id-ID") : "";
    }

    function handleInput(i: number, e: Event) {
        const target = e.target as HTMLInputElement;
        const rawValue = target.value.replace(/\D/g, "");
        wallets[i].amount = rawValue;
        target.value = formatCurrency(rawValue);
    }

    function handleSubmit() {
        window.location.href = "/app/dashboard";
    }
</script>

<svelte:head>
    <title>Setup Awal - Finance Pasut</title>
</svelte:head>

<div class="min-h-screen bg-slate-50 p-6 flex flex-col pt-12 pb-24">
    <div class="max-w-md w-full mx-auto flex flex-col h-full">
        <!-- Header -->
        <div class="mb-8 flex items-center justify-between">
            <a
                href="javascript:history.back()"
                class="text-gray-500 flex items-center hover:text-emerald-700 p-2 -ml-2"
            >
                <span class="text-xl">←</span>
            </a>
            <span class="font-semibold text-gray-800">Setup Awal</span>
            <span
                class="text-sm font-medium text-emerald-600 bg-emerald-50 px-3 py-1 rounded-full"
                >1 / 3</span
            >
        </div>

        <!-- Progress Bar -->
        <div
            class="w-full h-1.5 bg-gray-200 rounded-full mb-10 overflow-hidden"
        >
            <div
                class="h-full bg-emerald-500 w-1/3 rounded-full transition-all duration-500"
            ></div>
        </div>

        <!-- Content -->
        <div class="flex flex-col gap-8 mb-auto">
            <div class="flex flex-col gap-2">
                <h2
                    class="text-2xl font-bold text-gray-900 flex items-center gap-2"
                >
                    💰 Saldo Awal
                </h2>
                <p class="text-gray-600">
                    Masukkan saldo nyata saat ini untuk mulai mencatat keuangan
                    Anda:
                </p>
            </div>

            <div class="flex flex-col gap-5">
                {#each wallets as wallet, i (wallet.id)}
                    <div
                        class="flex flex-col gap-2 relative bg-white p-4 rounded-xl border border-gray-100 shadow-sm transition-all hover:border-emerald-200"
                    >
                        <div class="flex justify-between items-center mb-1">
                            {#if wallet.id > 3}
                                <!-- Editable name for custom wallets -->
                                <input
                                    type="text"
                                    bind:value={wallet.name}
                                    class="font-medium text-gray-700 bg-transparent border-b border-dashed border-gray-300 focus:border-emerald-500 focus:outline-none w-2/3"
                                    placeholder="Nama Dompet"
                                />
                            {:else}
                                <label class="font-medium text-gray-700 text-sm"
                                    >{wallet.name}</label
                                >
                            {/if}

                            {#if wallet.id > 3}
                                <button
                                    type="button"
                                    class="text-gray-400 hover:text-red-500 p-1"
                                    on:click={() => removeWallet(wallet.id)}
                                >
                                    ✕
                                </button>
                            {/if}
                        </div>

                        <div class="relative flex items-center">
                            <span
                                class="absolute left-4 font-medium text-gray-500 pointer-events-none"
                                >Rp</span
                            >
                            <input
                                type="text"
                                inputmode="numeric"
                                class="w-full bg-slate-50 border border-gray-200 rounded-lg h-12 pl-12 pr-4 text-gray-900 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-colors"
                                placeholder="0"
                                value={formatCurrency(wallet.amount)}
                                on:input={(e) => handleInput(i, e)}
                            />
                        </div>
                    </div>
                {/each}
            </div>

            <button
                type="button"
                class="flex items-center justify-center gap-2 mt-2 p-4 rounded-xl border-2 border-dashed border-emerald-200 text-emerald-600 font-medium hover:bg-emerald-50/50 hover:border-emerald-300 transition-colors"
                on:click={addWallet}
            >
                <span>+</span> Tambah Dompet Lain
            </button>
        </div>

        <!-- Fixed Bottom Action -->
        <div
            class="fixed bottom-0 left-0 right-0 p-6 bg-gradient-to-t from-slate-50 via-slate-50 to-transparent"
        >
            <div class="max-w-md mx-auto">
                <Button
                    fullWidth
                    size="lg"
                    on:click={handleSubmit}
                    classProp="shadow-lg shadow-emerald-500/20"
                >
                    LANJUT →
                </Button>
            </div>
        </div>
    </div>
</div>
