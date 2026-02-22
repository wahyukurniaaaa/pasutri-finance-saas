<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";
    import Input from "$lib/components/ui/Input.svelte";

    let name = "";
    let email = "";
    let password = "";
    let confirmPassword = "";
    let agreeTerms = false;

    // Realtime validation
    $: passwordLength = password.length >= 8;
    $: passwordAlphanumeric =
        /[a-zA-Z]/.test(password) && /[0-9]/.test(password);
    $: passwordMatch =
        password === confirmPassword && confirmPassword.length > 0;
    $: isValid =
        name.length >= 2 &&
        email.includes("@") &&
        passwordLength &&
        passwordAlphanumeric &&
        passwordMatch &&
        agreeTerms;

    function handleRegister() {
        window.location.href = "/onboarding/role";
    }
</script>

<svelte:head>
    <title>Daftar - Finance Pasut</title>
</svelte:head>

<div class="min-h-screen bg-slate-50 p-6 flex flex-col pt-8 pb-12">
    <div class="max-w-md w-full mx-auto">
        <!-- Header -->
        <div class="mb-8 flex flex-col gap-4">
            <a
                href="/"
                class="text-gray-500 flex items-center gap-2 hover:text-emerald-700 w-fit"
            >
                <span class="text-xl">←</span> Kembali
            </a>

            <div class="flex flex-col gap-2">
                <div class="text-3xl">💑</div>
                <h1 class="text-2xl font-bold text-gray-900">Buat Akun Baru</h1>
            </div>
        </div>

        <!-- Form -->
        <form
            class="flex flex-col gap-5"
            on:submit|preventDefault={handleRegister}
        >
            <Input
                type="text"
                bind:value={name}
                label="Nama Lengkap"
                placeholder="John Doe"
                iconClass="text-lg opacity-60">👤</Input
            >

            <Input
                type="email"
                bind:value={email}
                label="Email"
                placeholder="nama@email.com"
                iconClass="text-lg opacity-60">📧</Input
            >

            <div class="flex flex-col gap-2">
                <Input
                    type="password"
                    bind:value={password}
                    label="Password"
                    placeholder="••••••••"
                    iconClass="text-lg opacity-60">🔒</Input
                >

                <div
                    class="bg-white p-3 rounded-lg border border-gray-100 shadow-sm text-xs space-y-1.5 flex flex-col mx-1"
                >
                    <div
                        class="flex items-center gap-2 {passwordLength
                            ? 'text-emerald-600'
                            : 'text-gray-500'}"
                    >
                        <span class="font-bold"
                            >{passwordLength ? "✓" : "○"}</span
                        > Min 8 karakter
                    </div>
                    <div
                        class="flex items-center gap-2 {passwordAlphanumeric
                            ? 'text-emerald-600'
                            : 'text-gray-500'}"
                    >
                        <span class="font-bold"
                            >{passwordAlphanumeric ? "✓" : "○"}</span
                        > Huruf & angka
                    </div>
                </div>
            </div>

            <Input
                type="password"
                bind:value={confirmPassword}
                label="Konfirmasi Password"
                placeholder="••••••••"
                iconClass="text-lg opacity-60"
                error={!passwordMatch && confirmPassword
                    ? "Password tidak sama"
                    : ""}>🔒</Input
            >

            <label class="flex items-start gap-3 mt-2 cursor-pointer">
                <input
                    type="checkbox"
                    bind:checked={agreeTerms}
                    class="mt-1 w-4 h-4 text-emerald-600 rounded border-gray-300 focus:ring-emerald-500"
                />
                <span class="text-sm text-gray-600">
                    Saya setuju dengan <a
                        href="#"
                        class="text-emerald-600 font-medium hover:underline"
                        >Syarat & Ketentuan</a
                    >
                </span>
            </label>

            <div class="mt-4">
                <Button fullWidth type="submit" disabled={!isValid}
                    >DAFTAR</Button
                >
            </div>
        </form>

        <div class="my-6 flex items-center">
            <div class="flex-grow border-t border-gray-200"></div>
            <span class="px-4 text-sm text-gray-400">atau</span>
            <div class="flex-grow border-t border-gray-200"></div>
        </div>

        <Button variant="outline" fullWidth classProp="gap-3">
            <span class="text-xl">🔵</span> Daftar dengan Google
        </Button>

        <p class="mt-6 text-center text-sm text-gray-600">
            Sudah punya akun?
            <a
                href="/auth/login"
                class="font-medium text-emerald-600 hover:text-emerald-500"
                >Masuk</a
            >
        </p>
    </div>
</div>
