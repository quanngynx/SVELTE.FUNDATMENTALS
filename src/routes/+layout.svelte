<script lang="ts">
	import { page } from '$app/state';
	import { locales, localizeHref } from '$lib/paraglide/runtime';
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	import { ModeWatcher, resetMode, setMode } from "mode-watcher";

	import SunIcon from "@lucide/svelte/icons/sun";
    import MoonIcon from "@lucide/svelte/icons/moon";

	import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";
	import { buttonVariants } from "$lib/components/ui/button/index.js";

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<DropdownMenu.Root>
	<DropdownMenu.Trigger
	  class={buttonVariants({ variant: "outline", size: "icon" })}
	>
	  <SunIcon
		class="transition-all! h-[1.2rem] w-[1.2rem] rotate-0 scale-100 dark:-rotate-90 dark:scale-0"
	  />
	  <MoonIcon
		class="transition-all! absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 dark:rotate-0 dark:scale-100"
	  />
	  <span class="sr-only">Toggle theme</span>
	</DropdownMenu.Trigger>
	<DropdownMenu.Content align="end">
	  <DropdownMenu.Item onclick={() => setMode("light")}>Light</DropdownMenu.Item
	  >
	  <DropdownMenu.Item onclick={() => setMode("dark")}>Dark</DropdownMenu.Item>
	  <DropdownMenu.Item onclick={() => resetMode()}>System</DropdownMenu.Item>
	</DropdownMenu.Content>
  </DropdownMenu.Root>

<ModeWatcher />
{@render children()}
<div style="display:none">
	{#each locales as locale}
		<a href={localizeHref(page.url.pathname, { locale })}>
			{locale}
		</a>
	{/each}
</div>
