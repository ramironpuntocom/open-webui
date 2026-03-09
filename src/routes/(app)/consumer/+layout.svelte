<script lang="ts">
	import { onMount, getContext } from 'svelte';
	import { WEBUI_NAME, showSidebar, mobile } from '$lib/stores';
	import { page } from '$app/stores';
	import Tooltip from '$lib/components/common/Tooltip.svelte';
	import Sidebar from '$lib/components/icons/Sidebar.svelte';

	const i18n = getContext('i18n');

	let loaded = false;

	onMount(async () => {
		loaded = true;
	});
</script>

<svelte:head>
	<title>
		Espacio Consumer • {$WEBUI_NAME}
	</title>
</svelte:head>

{#if loaded}
	<div
		class=" relative flex flex-col w-full h-screen max-h-[100dvh] transition-width duration-200 ease-in-out {$showSidebar
			? 'md:max-w-[calc(100%-var(--sidebar-width))]'
			: ''} max-w-full"
	>
		<nav
			class="px-6 py-3 bg-[var(--topbar-bg)] text-[var(--topbar-text)] border-b border-[var(--topbar-border)] sticky top-0 z-40 backdrop-blur shadow-sm drag-region select-none"
		>
			<div class=" flex items-center gap-1">
				{#if $mobile}
					<div class="{$showSidebar ? 'md:hidden' : ''} self-center flex flex-none items-center">
						<Tooltip
							content={$showSidebar ? $i18n.t('Close Sidebar') : $i18n.t('Open Sidebar')}
							interactive={true}
						>
							<button
								id="sidebar-toggle-button"
								class="cursor-pointer flex rounded-lg hover:bg-[var(--topbar-border)] transition cursor- text-[var(--topbar-text)]"
								aria-label={$showSidebar ? $i18n.t('Close Sidebar') : $i18n.t('Open Sidebar')}
								on:click={() => {
									showSidebar.set(!$showSidebar);
								}}
							>
								<div class=" self-center p-1.5">
									<Sidebar />
								</div>
							</button>
						</Tooltip>
					</div>
				{/if}

				<div class="">
					<div
						class="flex gap-1 scrollbar-none overflow-x-auto w-fit text-center text-sm font-medium rounded-full bg-transparent py-1 touch-auto pointer-events-auto"
					>
						<a
							draggable="false"
							aria-current={$page.url.pathname.includes('/consumer/kpi-consumer') ? 'page' : null}
							class="min-w-fit px-2 py-1 border-b-2 {$page.url.pathname.includes('/consumer/kpi-consumer')
								? 'font-semibold border-[var(--sidebar-active)] text-[var(--topbar-text)]'
								: 'border-transparent text-[var(--topbar-text)] hover:text-[var(--sidebar-text)]'} transition select-none"
							href="/consumer/kpi-consumer"
						>
							KPI Consumer
						</a>

						<a
							draggable="false"
							aria-current={$page.url.pathname.includes('/consumer/bench-mora-tardia')
								? 'page'
								: null}
							class="min-w-fit px-2 py-1 border-b-2 {$page.url.pathname.includes('/consumer/bench-mora-tardia')
								? 'font-semibold border-[var(--sidebar-active)] text-[var(--topbar-text)]'
								: 'border-transparent text-[var(--topbar-text)] hover:text-[var(--sidebar-text)]'} transition select-none"
							href="/consumer/bench-mora-tardia"
						>
							BENCH Mora Tardía
						</a>
					</div>
				</div>
			</div>
		</nav>

		<div class="pb-1 px-3 md:px-[18px] flex-1 max-h-full overflow-y-auto" id="consumer-container">
			<slot />
		</div>
	</div>
{/if}
