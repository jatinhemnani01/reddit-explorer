<script>
  export let title = "";
  export let img_url = "";
</script>

<div class="card-container">
  <div class="card-title">{title}</div>
  <img onerror="this.style.display='none'" src={img_url} alt="" />
</div>
