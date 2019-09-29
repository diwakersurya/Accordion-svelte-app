<script>
  import { createEventDispatcher, setContext } from "svelte";
  import { writable } from "svelte/store";
  const accordionStore = writable(null);
  import Section from "./AccordionSection.svelte";
  export let value;
  accordionStore.set(value);
  console.log($accordionStore);
  const isControlled = typeof $accordionStore !== "undefined";

  const dispatch = createEventDispatcher();
  const handleChange = function(newValue) {
    if (!isControlled) {
      value = newValue;
    }
    dispatch("change", newValue);
  };
  setContext("accordion", { handleChange, accordionStore });
</script>

<style>
  .accordion {
    list-style: none;
  }
</style>

<ul class="accordion">
  <slot {value} />
</ul>
