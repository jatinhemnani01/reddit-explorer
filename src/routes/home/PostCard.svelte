<script>
  export let title = "";
  export let img_url = "";
</script>

<div class="card-container">
  <div class="card-title">{title}</div>
  <img onerror="this.style.display='none'" src={img_url} alt="" />
</div>

<style>
  .card-container {
    border: solid 1px orange;
    padding: 1em;
  }
  .card-container img {
    width: 30%;
    margin: auto;
    display: flex;
  }
</style>
