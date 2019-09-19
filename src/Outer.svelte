<script>
  import Inner from "./Inner.svelte";
  import { createEventDispatcher } from "svelte";

  let count = 0;

  const dispatch = createEventDispatcher();

  function forward(event) {
    console.log(event);
    count += event.detail.increment;
    dispatch("count", { count: count });
  }
</script>

<Inner on:message={forward} />
