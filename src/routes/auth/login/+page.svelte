<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";
    import Input from "$lib/components/ui/Input.svelte";

    let email = "";
    let password = "";

    function handleLogin() {
        // Navigate to role selection or dashboard
        window.location.href = "/onboarding/role";
    }
</script>

<svelte:head>
    <title>Masuk - Finance Pasut</title>
</svelte:head>

<div class="min-h-screen bg-slate-50 p-6 flex flex-col pt-12">
    <div class="max-w-md w-full mx-auto">
        <!-- Header -->
        <div class="mb-10 flex flex-col gap-6">
            <a
                href="/"
                class="text-gray-500 flex items-center gap-2 hover:text-emerald-700 w-fit"
            >
                <span class="text-xl">←</span> Kembali
            </a>

            <div class="flex flex-col gap-2">
                <div class="text-3xl">💑</div>
                <h1 class="text-2xl font-bold text-gray-900">Masuk ke Akun</h1>
            </div>
        </div>

        <!-- Form -->
        <form
            class="flex flex-col gap-5"
            on:submit|preventDefault={handleLogin}
        >
            <Input
                type="email"
                bind:value={email}
                label="Email"
                placeholder="nama@email.com"
                iconClass="text-lg opacity-60">📧</Input
            >

            <div class="flex flex-col gap-1">
                <Input
                    type="password"
                    bind:value={password}
                    label="Password"
                    placeholder="••••••••"
                    iconClass="text-lg opacity-60">🔒</Input
                >
                <div class="flex justify-end mt-1">
                    <a
                        href="#"
                        class="text-sm font-medium text-emerald-600 hover:text-emerald-500"
                    >Lupa password?</a>
                </div>
            </div>

            <div class="mt-4">
                <Button fullWidth type="submit" disabled={!email || !password}
                >MASUK</Button>
            </div>
        </form>

        <div class="my-8 flex items-center">
            <div class="flex-grow border-t border-gray-200"></div>
            <span class="px-4 text-sm text-gray-400">atau</span>
            <div class="flex-grow border-t border-gray-200"></div>
        </div>

        <Button variant="outline" fullWidth classProp="gap-3">
            <span class="text-xl">🔵</span> Lanjutkan dengan Google
        </Button>

        <p class="mt-8 text-center text-sm text-gray-600">
            Belum punya akun?
            <a
                href="/auth/register"
                class="font-medium text-emerald-600 hover:text-emerald-500"
            >Daftar</a>
        </p>
    </div>
</div>
