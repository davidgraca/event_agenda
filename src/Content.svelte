<script>
  import { getContext } from "svelte";
  import Surprise from "./Surprise.svelte";
  export let info, showModal;

  const { open } = getContext("simple-modal");

  $: {
    console.log(info);
    if (showModal == true) open(Surprise, {allData:info});
  }
</script>