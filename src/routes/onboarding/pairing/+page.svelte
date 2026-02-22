<script lang="ts">
    import Button from "$lib/components/ui/Button.svelte";

    // Note: in a real app, 'mode' would come from page store $page.url.searchParams
    // For UI mockup, we'll just mock it or assume generate mode by default
    let mode: "generate" | "input" = "generate";

    // Fake pairing code state
    let generatedCode = "ABC-123-XYZ";
    let isCopied = false;

    // For input mode
    let inputCode = ["", "", "", "", "", ""]; // Represents ABC 123
    let inputError = false;

    function copyCode() {
        navigator.clipboard.writeText(generatedCode);
        isCopied = true;
        setTimeout(() => (isCopied = false), 2000);
    }

    function handleInput(index: number, e: Event) {
        const target = e.target as HTMLInputElement;
        const value = target.value.toUpperCase();

        // Only alphanumeric
        if (/^[A-Z0-9]$/.test(value)) {
            inputCode[index] = value;
            // move to next
            if (index < 5) {
                document.getElementById(`code-${index + 1}`)?.focus();
            }
        } else {
            target.value = inputCode[index] || "";
        }
        inputCode = [...inputCode];
        inputError = false;
    }

    function handleKeydown(index: number, e: KeyboardEvent) {
        if (e.key === "Backspace") {
            if (!inputCode[index] && index > 0) {
                document.getElementById(`code-${index - 1}`)?.focus();
            }
            inputCode[index] = "";
            inputCode = [...inputCode];
            inputError = false;
        }
    }

    function handleSubmit() {
        const fullCode = inputCode.join("");
        if (fullCode.length !== 6) {
            inputError = true;
            return;
        }
        // Success -> proceed to setup
        window.location.href = "/onboarding/setup";
    }
</script>

<svelte:head>
    <title>Hubungkan Pasangan - Finance Pasut</title>
</svelte:head>

<div class="min-h-screen bg-slate-50 p-6 flex flex-col pt-12">
    <div class="max-w-md w-full mx-auto flex flex-col h-full min-h-[80vh]">
        <!-- Header -->
        <div class="mb-10 flex flex-col gap-6">
            <a
                href="javascript:history.back()"
                class="text-gray-500 flex items-center gap-2 hover:text-emerald-700 w-fit"
            >
                <span class="text-xl">←</span> Hubungkan Pasangan
            </a>

            <div class="flex flex-col gap-3">
                <div class="text-4xl text-emerald-500">🔗</div>
            </div>
        </div>

        {#if mode === "generate"}
            <div class="flex flex-col gap-6 mb-auto animate-fade-in">
                <p class="text-gray-700 text-lg">
                    Bagikan kode ini ke pasangan Anda untuk terhubung:
                </p>

                <div
                    class="bg-white border-2 border-emerald-100 rounded-2xl p-6 flex flex-col items-center gap-4 shadow-sm relative overflow-hidden"
                >
                    <div
                        class="absolute inset-0 bg-emerald-50 opacity-50"
                    ></div>
                    <div
                        class="relative z-10 font-mono text-4xl font-bold tracking-[0.2em] text-gray-900 drop-shadow-sm"
                    >
                        {generatedCode}
                    </div>
                </div>

                <div class="flex justify-center -mt-2">
                    <button
                        on:click={copyCode}
                        class="text-emerald-600 font-medium flex items-center gap-2 hover:text-emerald-700 transition-colors"
                    >
                        📋 {isCopied ? "Tersalin!" : "Salin Kode"}
                    </button>
                </div>

                <p class="text-sm text-gray-500 text-center mt-4">
                    Kode berlaku selama 24 jam
                </p>

                <Button
                    variant="outline"
                    fullWidth
                    classProp="gap-3 mt-4 border-emerald-200 bg-emerald-50/50 hover:bg-emerald-50 text-emerald-800"
                >
                    <span class="text-lg">📤</span> Bagikan via WhatsApp
                </Button>

                <div
                    class="flex flex-col items-center gap-3 mt-12 bg-white p-6 rounded-2xl border border-gray-100 shadow-sm"
                >
                    <div
                        class="w-8 h-8 rounded-full border-2 border-emerald-200 border-t-emerald-500 animate-spin"
                    ></div>
                    <div class="text-sm text-gray-600 font-medium">
                        Menunggu pasangan...
                    </div>
                    <div class="text-xs text-gray-400">
                        Auto-refresh tiap 5 detik
                    </div>

                    <!-- DEV ONLY: Button to simulate mock flow -->
                    <a
                        href="/onboarding/setup"
                        class="text-xs text-blue-500 mt-4 underline"
                        >Dev: Skip wait</a
                    >
                </div>
            </div>
        {:else}
            <div class="flex flex-col gap-6 mb-auto animate-fade-in">
                <p class="text-gray-700 text-lg">
                    Masukkan kode dari pasangan Anda:
                </p>

                <div class="flex items-center justify-center gap-2 mt-4">
                    <!-- 3 chars -->
                    {#each Array(3) as _, i}
                        <input
                            id={`code-${i}`}
                            type="text"
                            maxlength="1"
                            value={inputCode[i]}
                            on:input={(e) => handleInput(i, e)}
                            on:keydown={(e) => handleKeydown(i, e)}
                            class="w-12 h-16 text-center text-2xl font-bold font-mono rounded-xl border-2 {inputError
                                ? 'border-red-400 bg-red-50'
                                : 'border-gray-200 focus:border-emerald-500 focus:ring-emerald-500'} bg-white"
                        />
                    {/each}

                    <div class="w-4 h-1 bg-gray-300 rounded-full mx-1"></div>

                    <!-- 3 chars -->
                    {#each Array(3) as _, i}
                        {@const index = i + 3}
                        <input
                            id={`code-${index}`}
                            type="text"
                            maxlength="1"
                            value={inputCode[index]}
                            on:input={(e) => handleInput(index, e)}
                            on:keydown={(e) => handleKeydown(index, e)}
                            class="w-12 h-16 text-center text-2xl font-bold font-mono rounded-xl border-2 {inputError
                                ? 'border-red-400 bg-red-50'
                                : 'border-gray-200 focus:border-emerald-500 focus:ring-emerald-500'} bg-white"
                        />
                    {/each}
                </div>

                {#if inputError}
                    <p
                        class="text-red-500 text-sm text-center font-medium my-2 animate-pulse"
                    >
                        ⚠️ Kode tidak ditemukan atau kadaluarsa
                    </p>
                {/if}
            </div>

            <div class="mt-8 pt-8">
                <Button
                    fullWidth
                    size="lg"
                    on:click={handleSubmit}
                    disabled={inputCode.join("").length !== 6}
                >
                    HUBUNGKAN
                </Button>
            </div>
        {/if}
    </div>
</div>
