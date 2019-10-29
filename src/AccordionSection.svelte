<script>
  import {
    createEventDispatcher,
    getContext,
    onMount,
    onDestroy
  } from "svelte";
  import { ACCORDION } from "./Accordion.svelte";
  import { slide } from "svelte/transition";
  import Header from "./AccordionHeader.svelte";
  export let title = "header title";
  export let open = false;
  const { handleChange, selected } = getContext(ACCORDION);
  //get selected value from context
  $: open = $selected === title;
  export let onHeaderClick;
</script>

<li className="accordion-section">
  <Header on:click={handleChange.bind(null, title)} {title} {open} />
  {#if open}
    <div transition:slide>
      <slot />
    </div>
  {/if}
</li>
