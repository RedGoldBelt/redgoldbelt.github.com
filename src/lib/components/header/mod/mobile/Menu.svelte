<script lang="ts">
    import { slide } from "svelte/transition";
    import Chevron from "$lib/components/Chevron.svelte";
    import { afterNavigate } from "$app/navigation";

    interface Props {
        open: boolean;
    }

    let { open = $bindable() }: Props = $props();
    let issuesOpen = $state(false);

    const closeMenu = () => {
        open = false;
        issuesOpen = false;
    };

    afterNavigate(closeMenu);
</script>

{#if open}
    <menu class="fixed top-12 left-0 w-screen bg-amber-100 shadow-xl" transition:slide>
        <a class="block p-4 group" onclick={closeMenu} href="/">
            <span class="link nav-link">Home</span>
        </a>
        <a class="block p-4 group" onclick={closeMenu} href="/about">
            <span class="link nav-link">About</span>
        </a>
        <button class="block w-full text-left p-4 group" onclick={() => (issuesOpen = !issuesOpen)}>
            <span class="nav-link">
                Issues <Chevron up={issuesOpen} />
            </span>
        </button>
        {#if issuesOpen}
            <menu class="ml-8" transition:slide>
                <a class="block p-2 group" href="/archive">
                    <span class="link nav-link">Archive</span>
                </a>
                <a class="block p-2 group" href="/bibliography">
                    <span class="link nav-link">Bibliography</span>
                </a>
                <a class="block p-2 group" href="/puzzles">
                    <span class="link nav-link">Puzzles</span>
                </a>
            </menu>
        {/if}
        <a class="block p-4 group" onclick={closeMenu} href="/events">
            <span class="link nav-link">Events</span>
        </a>
    </menu>
{/if}

<style lang="postcss">
    .nav-link {
        @apply text-xl tracking-wider text-cyan-800 hover:text-cyan-600;
    }
</style>
