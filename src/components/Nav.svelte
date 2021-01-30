<script>
  export let segment;
</script>

<nav>
  <a class={segment === "home" ? "page" : undefined} href="/home">Home</a>
  <a class={segment === "contact" ? "page" : undefined} href="/contact"
    >Contact</a
  >
  <a class={segment === "donate" ? "page" : undefined} href="/donate">Donate</a>
</nav>

<style>
  nav {
    margin: 0px;
    display: flex;
    flex-wrap: wrap;
    padding: 1em;
    background-color: cyan;
  }
  nav a {
    margin: 0.5em;
    text-decoration: none;
    color: black;
  }
  .page {
    border-bottom: solid 1px orange;
  }
</style>
