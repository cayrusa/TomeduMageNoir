<script lang="ts">
    import { page } from "$app/stores";
    import type { Decks } from "$lib/Decks.svelte.js";
    import { sanitizeElement } from "$lib/utils.js";
    let { number, card } = $props();
    let decks: Decks = $page.data.decks;
</script>

<td class="minimize"
    ><button type="button" onclick={() => decks.activeDeck.delCard(card)}>
        🗑️
    </button>
</td>
<td class="minimize">
    <button type="button" onclick={() => decks.activeDeck.modCard(card, -1)}>
        -
    </button>
    {number}
    <button type="button" onclick={() => decks.activeDeck.modCard(card, 1)}>
        +
    </button>
</td>
<td class="name">
    {#if card.url_to_collection_page}
    <a
        href="{card.url_to_collection_page}"
        target="_blank"
    >
        {card.name}
        {#if card.transmutables.length > 0}
            ({card.transmutables.substring(1)})
        {/if}
    </a>
    {:else}
    <a
        href="https://magenoir.com/collection/{card.language.toUpperCase()}/{sanitizeElement(
            card.element,
        )}/{card.slug}.html"
        target="_blank"
    >
        {card.name}
        {#if card.transmutables.length > 0}
            ({card.transmutables.substring(1)})
        {/if}
    </a>
    {/if}
</td>

<style>
    button
    {
        border: none;
        border-radius: 5px;
        width: 25px;
        height: 25px;
        text-align: center;
    }

    button:hover
    {
        cursor: pointer;
    }
    td.minimize {
        width: 10px;
    }
    td.name a {
        display: block;
        text-transform: lowercase;
    }
    td.name a::first-letter {
        text-transform: capitalize;
    }
</style>