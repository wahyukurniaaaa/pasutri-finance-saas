<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";
    import Card from "$lib/components/ui/Card.svelte";
</script>

<svelte:head>
    <title>Finance Pasut - Kelola Keuangan Bersama</title>
</svelte:head>

<div
    class="min-h-screen bg-slate-50 flex flex-col items-center justify-center p-6 bg-gradient-to-br from-emerald-50 to-teal-100"
>
    <div class="w-full max-w-md flex flex-col items-center gap-8">
        <!-- Logo & Brand -->
        <div class="flex flex-col items-center gap-3">
            <div class="text-6xl animate-bounce">💑</div>
            <h1
                class="text-3xl font-bold bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent"
            >
                Finance Pasut
            </h1>
            <p class="text-gray-600 text-center text-sm px-4">
                Platform cerdas untuk mengelola keuangan rumah tangga secara
                kolaboratif.
            </p>
        </div>

        <!-- Hero Card -->
        <Card glass classProp="w-full">
            <h2
                class="text-xl font-semibold text-gray-800 mb-4 flex items-center gap-2"
            >
                <span>✨</span> Kelola Keuangan Bersama Pasangan
            </h2>

            <ul class="space-y-3 mb-6">
                <li class="flex items-center gap-3 text-gray-700">
                    <span
                        class="text-emerald-500 bg-emerald-100 p-1 rounded-full text-xs"
                        >✓</span
                    >
                    Transparansi penuh pengeluaran
                </li>
                <li class="flex items-center gap-3 text-gray-700">
                    <span
                        class="text-emerald-500 bg-emerald-100 p-1 rounded-full text-xs"
                        >✓</span
                    >
                    Pantau tujuan / tabungan bersama
                </li>
                <li class="flex items-center gap-3 text-gray-700">
                    <span
                        class="text-emerald-500 bg-emerald-100 p-1 rounded-full text-xs"
                        >✓</span
                    >
                    Satu dashboard untuk berdua
                </li>
            </ul>

            <div class="flex flex-col gap-4 mt-8">
                <a href="/auth/register" class="w-full block">
                    <Button fullWidth size="lg">MULAI SEKARANG</Button>
                </a>

                <p class="text-center text-sm text-gray-500">
                    Sudah punya akun?
                    <a
                        href="/auth/login"
                        class="text-emerald-600 font-medium hover:underline"
                        >Masuk</a
                    >
                </p>
            </div>
        </Card>
    </div>
</div>
