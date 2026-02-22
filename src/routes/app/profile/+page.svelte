<script lang="ts">
    import Card from "$lib/components/ui/Card.svelte";
    import Button from "$lib/components/ui/Button.svelte";
</script>

<svelte:head>
    <title>Profil Pasangan - Finance Pasut</title>
</svelte:head>

<div class="p-6 pt-12 flex flex-col gap-6">
    <!-- Header -->
    <div class="flex justify-between items-center mb-2">
        <h1 class="text-2xl font-bold text-gray-900 flex items-center gap-2">
            👤 Profil
        </h1>
        <button class="text-gray-500 font-medium text-sm hover:underline"
            >⚙️ Pengaturan</button
        >
    </div>

    <Card classProp="flex flex-col gap-4 text-center items-center py-8">
        <div class="flex items-center gap-2 mb-2">
            <div
                class="w-20 h-20 rounded-full bg-emerald-100 flex items-center justify-center text-4xl shadow-inner border-4 border-white"
            >
                👨
            </div>
            <div
                class="w-20 h-20 rounded-full bg-rose-100 flex items-center justify-center text-4xl shadow-inner border-4 border-white -ml-6 relative z-10"
            >
                👩
            </div>
        </div>

        <div>
            <h2 class="text-xl font-bold text-gray-900">
                Keluarga Bapak Wahyu
            </h2>
            <p class="text-xs text-gray-500 mt-1">
                Status: Terhubung (Sejak Nov 2024)
            </p>
        </div>
    </Card>

    <div class="flex flex-col gap-3">
        <h3 class="font-bold text-gray-800">Manajemen Dompet</h3>

        <div
            class="bg-white p-4 rounded-xl border border-gray-100 shadow-sm flex items-center justify-between"
        >
            <div class="flex items-center gap-3">
                <div class="text-2xl mx-1">🏦</div>
                <div class="flex flex-col">
                    <span class="font-bold text-gray-900"
                        >Rekening Bersama (BCA)</span
                    >
                    <span class="text-xs text-gray-500 font-medium"
                        >Dana Darurat & KPR</span
                    >
                </div>
            </div>
        </div>

        <div
            class="bg-white p-4 rounded-xl border border-gray-100 shadow-sm flex items-center justify-between"
        >
            <div class="flex items-center gap-3">
                <div class="text-2xl mx-1">💳</div>
                <div class="flex flex-col">
                    <span class="font-bold text-gray-900"
                        >Kas Istri (Mandiri)</span
                    >
                    <span class="text-xs text-gray-500 font-medium"
                        >Dapur & Anak</span
                    >
                </div>
            </div>
        </div>

        <button
            class="w-full mt-2 py-3 rounded-xl border-2 border-dashed border-gray-200 text-gray-500 font-medium text-sm hover:bg-gray-50 transition-colors"
        >
            + Tambah Dompet Baru
        </button>
    </div>

    <div class="mt-8">
        <Button
            variant="outline"
            fullWidth
            classProp="text-rose-500 border-rose-200 hover:bg-rose-50 hover:border-rose-300"
        >
            KELUAR AKUN
        </Button>
    </div>
</div>
