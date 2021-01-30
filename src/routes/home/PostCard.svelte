<script>
  export let title = "";
  export let img_url = "";
  export let desc = "";
  export let url = "";
</script>

<a href={url} target="_blank">
  <div class="card-container">
    <div class="card-title">{title}</div>
    <img onerror="this.style.display='none'" src={img_url} alt="" />
    <!-- svelte-ignore a11y-media-has-caption -->

    <div class="card-desc">{desc}</div>
  </div>
</a>

<style>
  a {
    text-decoration: none;
    color: #b9d8ff;
  }
  .card-container {
    border: solid 1px orange;
    padding: 1em;
  }
  .card-container img {
    width: 40%;
    margin: auto;
    display: flex;
  }
  .card-title {
    font-size: 1.2em;
    font-weight: bold;
    padding: 0.5em;
  }
  .card-desc {
    font-size: 1em;
    padding: 0.5em;
  }
  @media screen and (max-width: 670px) {
    img {
      width: 50%;
    }
  }
</style>
