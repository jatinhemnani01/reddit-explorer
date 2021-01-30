<script>
  // import Nav from "../components/Nav.svelte";

  export let segment;
  segment = !segment;
</script>

<!-- <Nav {segment} /> -->

<main>
  <slot />
</main>

<style>
  main {
    margin: 0px;
    padding: 0px;
  }
</style>
