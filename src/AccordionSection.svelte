<script>
  import {
    createEventDispatcher,
    getContext,
    onMount,
    onDestroy
  } from "svelte";
  import { slide } from "svelte/transition";
  import Header from "./AccordionHeader.svelte";
  export let title = "header title";
  export let open = false;
  let unsubscribe;
  const { accordionStore, handleChange } = getContext("accordion");

  const isControlled = typeof value !== "undefined";

  export let onHeaderClick;
  const dispatch = createEventDispatcher();
</script>

<li className="accordion-section">
  <Header on:click={handleChange.bind(null, title)} {title} {open} />
  {#if open}
    <div transition:slide>
      <slot />
    </div>
  {/if}
</li>
