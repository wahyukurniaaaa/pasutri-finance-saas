<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";

    let selectedRole: "Suami" | "Istri" | null = null;
</script>

<svelte:head>
    <title>Pilih Peran - Finance Pasut</title>
</svelte:head>

<div class="min-h-screen bg-slate-50 p-6 flex flex-col pt-12">
    <div class="max-w-md w-full mx-auto flex flex-col h-full min-h-[80vh]">
        <!-- Header -->
        <div class="mb-10 flex flex-col gap-6">
            <a
                href="/auth/register"
                class="text-gray-500 flex items-center gap-2 hover:text-emerald-700 w-fit"
            >
                <span class="text-xl">←</span>
            </a>

            <div class="flex flex-col gap-3">
                <h1
                    class="text-3xl font-bold bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent"
                >
                    🎉 Selamat Datang!
                </h1>
                <p class="text-gray-600 text-lg">
                    Pilih peran Anda dalam hubungan ini:
                </p>
            </div>
        </div>

        <!-- Role Selection -->
        <div class="grid grid-cols-2 gap-4 mb-10">
            <button
                class="flex flex-col items-center justify-center p-8 rounded-2xl border-2 transition-all {selectedRole ===
                'Suami'
                    ? 'border-emerald-500 bg-emerald-50 shadow-md ring-4 ring-emerald-50'
                    : 'border-gray-200 bg-white hover:border-gray-300 hover:bg-gray-50'}"
                on:click={() => (selectedRole = "Suami")}
            >
                <span class="text-5xl mb-4">👨‍💼</span>
                <span class="font-bold text-gray-900 text-lg">SUAMI</span>
                <div
                    class="mt-4 flex items-center gap-2 text-sm {selectedRole ===
                    'Suami'
                        ? 'text-emerald-600'
                        : 'text-gray-400'}"
                >
                    <div
                        class="w-4 h-4 rounded-full border-2 flex items-center justify-center {selectedRole ===
                        'Suami'
                            ? 'border-emerald-500'
                            : 'border-gray-300'}"
                    >
                        {#if selectedRole === "Suami"}
                            <div
                                class="w-2 h-2 rounded-full bg-emerald-500"
                            ></div>
                        {/if}
                    </div>
                    Pilih
                </div>
            </button>

            <button
                class="flex flex-col items-center justify-center p-8 rounded-2xl border-2 transition-all {selectedRole ===
                'Istri'
                    ? 'border-emerald-500 bg-emerald-50 shadow-md ring-4 ring-emerald-50'
                    : 'border-gray-200 bg-white hover:border-gray-300 hover:bg-gray-50'}"
                on:click={() => (selectedRole = "Istri")}
            >
                <span class="text-5xl mb-4">👩‍💼</span>
                <span class="font-bold text-gray-900 text-lg">ISTRI</span>
                <div
                    class="mt-4 flex items-center gap-2 text-sm {selectedRole ===
                    'Istri'
                        ? 'text-emerald-600'
                        : 'text-gray-400'}"
                >
                    <div
                        class="w-4 h-4 rounded-full border-2 flex items-center justify-center {selectedRole ===
                        'Istri'
                            ? 'border-emerald-500'
                            : 'border-gray-300'}"
                    >
                        {#if selectedRole === "Istri"}
                            <div
                                class="w-2 h-2 rounded-full bg-emerald-500"
                            ></div>
                        {/if}
                    </div>
                    Pilih
                </div>
            </button>
        </div>

        <div class="my-6 flex items-center">
            <div class="flex-grow border-t border-gray-200"></div>
            <span class="px-4 text-sm text-gray-400">atau</span>
            <div class="flex-grow border-t border-gray-200"></div>
        </div>

        <!-- Alternative -->
        <div class="flex flex-col items-center gap-4 mb-auto">
            <p class="text-gray-600 text-sm">Pasangan sudah daftar duluan?</p>
            <a href="/onboarding/pairing?mode=input" class="w-full">
                <Button variant="outline" fullWidth
                    >MASUKKAN KODE PASANGAN</Button
                >
            </a>
        </div>

        <!-- Actions -->
        <div class="mt-8 pt-8">
            <a
                href="/onboarding/pairing?mode=generate"
                class={!selectedRole ? "pointer-events-none" : ""}
            >
                <Button fullWidth disabled={!selectedRole} size="lg"
                    >LANJUTKAN</Button
                >
            </a>
        </div>
    </div>
</div>
