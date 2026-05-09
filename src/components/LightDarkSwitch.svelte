<script lang="ts">
import { AUTO_MODE, DARK_MODE, LIGHT_MODE } from "@constants/constants.ts";
import I18nKey from "@i18n/i18nKey";
import { i18n } from "@i18n/translation";
import {
	applyThemeToDocument,
	getStoredTheme,
	setTheme,
} from "@utils/setting-utils.ts";
import { onMount } from "svelte";
import type { LIGHT_DARK_MODE } from "@/types/config.ts";

let { hydrated = false }: { hydrated?: boolean } = $props();
void hydrated;

const seq: LIGHT_DARK_MODE[] = [LIGHT_MODE, DARK_MODE, AUTO_MODE];
let mode: LIGHT_DARK_MODE = $state(AUTO_MODE);

onMount(() => {
	mode = getStoredTheme();
	const darkModePreference = window.matchMedia("(prefers-color-scheme: dark)");
	const changeThemeWhenSchemeChanged: Parameters<
		typeof darkModePreference.addEventListener<"change">
	>[1] = (_e) => {
		applyThemeToDocument(mode);
	};
	darkModePreference.addEventListener("change", changeThemeWhenSchemeChanged);
	return () => {
		darkModePreference.removeEventListener(
			"change",
			changeThemeWhenSchemeChanged,
		);
	};
});

function switchScheme(newMode: LIGHT_DARK_MODE) {
	mode = newMode;
	setTheme(newMode);
}

function toggleScheme() {
	let i = 0;
	for (; i < seq.length; i++) {
		if (seq[i] === mode) {
			break;
		}
	}
	switchScheme(seq[(i + 1) % seq.length]);
}

function showPanel() {
	const panel = document.querySelector("#light-dark-panel");
	panel?.classList.remove("float-panel-closed");
}

function hidePanel() {
	const panel = document.querySelector("#light-dark-panel");
	panel?.classList.add("float-panel-closed");
}
</script>

<!-- z-50 make the panel higher than other float panels -->
<div class="relative z-50" role="menu" tabindex="-1" onmouseleave={hidePanel}>
    <button aria-label="切换明暗模式" role="menuitem" class="relative btn-plain scale-animation rounded-full h-10 w-10 active:scale-90" id="scheme-switch" onclick={toggleScheme} onmouseenter={showPanel}>
        <div class="absolute inset-0 flex items-center justify-center transition text-[var(--btn-content)]" class:opacity-0={mode !== LIGHT_MODE}>
            <svg aria-hidden="true" viewBox="0 0 24 24" class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="12" cy="12" r="4"></circle>
                <path d="M12 2v2"></path>
                <path d="M12 20v2"></path>
                <path d="m4.93 4.93 1.41 1.41"></path>
                <path d="m17.66 17.66 1.41 1.41"></path>
                <path d="M2 12h2"></path>
                <path d="M20 12h2"></path>
                <path d="m6.34 17.66-1.41 1.41"></path>
                <path d="m19.07 4.93-1.41 1.41"></path>
            </svg>
        </div>
        <div class="absolute inset-0 flex items-center justify-center transition text-[var(--btn-content)]" class:opacity-0={mode !== DARK_MODE}>
            <svg aria-hidden="true" viewBox="0 0 24 24" class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M20.4 14.5A8.2 8.2 0 0 1 9.5 3.6 8.5 8.5 0 1 0 20.4 14.5Z"></path>
            </svg>
        </div>
        <div class="absolute inset-0 flex items-center justify-center transition text-[var(--btn-content)]" class:opacity-0={mode !== AUTO_MODE}>
            <svg aria-hidden="true" viewBox="0 0 24 24" class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="12" cy="12" r="8"></circle>
                <path d="m9 16 3-8 3 8"></path>
                <path d="M10.2 13h3.6"></path>
            </svg>
        </div>
    </button>

    <div id="light-dark-panel" class="hidden lg:block absolute transition float-panel-closed top-11 -right-2 pt-5" >
        <div class="card-base float-panel p-2">
            <button class="flex transition whitespace-nowrap items-center !justify-start w-full btn-plain scale-animation rounded-lg h-9 px-3 font-medium active:scale-95 mb-0.5"
                    class:current-theme-btn={mode === LIGHT_MODE}
                    onclick={() => switchScheme(LIGHT_MODE)}
            >
                <svg aria-hidden="true" viewBox="0 0 24 24" class="mr-3 h-5 w-5 shrink-0" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="4"></circle>
                    <path d="M12 2v2"></path>
                    <path d="M12 20v2"></path>
                    <path d="m4.93 4.93 1.41 1.41"></path>
                    <path d="m17.66 17.66 1.41 1.41"></path>
                    <path d="M2 12h2"></path>
                    <path d="M20 12h2"></path>
                    <path d="m6.34 17.66-1.41 1.41"></path>
                    <path d="m19.07 4.93-1.41 1.41"></path>
                </svg>
                {i18n(I18nKey.lightMode)}
            </button>
            <button class="flex transition whitespace-nowrap items-center !justify-start w-full btn-plain scale-animation rounded-lg h-9 px-3 font-medium active:scale-95 mb-0.5"
                    class:current-theme-btn={mode === DARK_MODE}
                    onclick={() => switchScheme(DARK_MODE)}
            >
                <svg aria-hidden="true" viewBox="0 0 24 24" class="mr-3 h-5 w-5 shrink-0" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M20.4 14.5A8.2 8.2 0 0 1 9.5 3.6 8.5 8.5 0 1 0 20.4 14.5Z"></path>
                </svg>
                {i18n(I18nKey.darkMode)}
            </button>
            <button class="flex transition whitespace-nowrap items-center !justify-start w-full btn-plain scale-animation rounded-lg h-9 px-3 font-medium active:scale-95"
                    class:current-theme-btn={mode === AUTO_MODE}
                    onclick={() => switchScheme(AUTO_MODE)}
            >
                <svg aria-hidden="true" viewBox="0 0 24 24" class="mr-3 h-5 w-5 shrink-0" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="8"></circle>
                    <path d="m9 16 3-8 3 8"></path>
                    <path d="M10.2 13h3.6"></path>
                </svg>
                {i18n(I18nKey.systemMode)}
            </button>
        </div>
    </div>
</div>
