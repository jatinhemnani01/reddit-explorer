<script>
  // ALL IMPORTS
  import { onMount } from "svelte";
  import PostCard from "./PostCard.svelte";
  // ALL IMPORTS

  //   VARIABLES AND LISTS
  let posts = [];
  let isError = false;
  let subreddit = "wallstreetbets";
  let badge = "hot";
  let loading = true;

  //   VARIABLES AND LISTS

  //   GET REDDIT POSTS
  const getPost = async (subReddit, Badge) => {
    try {
      let res = await fetch(
        `https://www.reddit.com/r/${subReddit}/${Badge}.json?limit=10`
      );
      let data = await res.json();
      let post = data.data.children;
      posts = post;
      loading = false;
      isError = false;
    } catch (error) {
      isError = true;
    }
  };
  //   GET REDDIT POSTS

  // ONMOUNT

  onMount(() => {
    getPost(subreddit, badge);
  });
  // ONMOUNT

  //   FORM SUBMIT FUNCTIONS
  const handleSubmit = () => {
    loading = true;
    getPost(subreddit, badge);
    loading = false;
  };
  //   FORM SUBMIT FUNCTIONS

  // BADGE HANDLE (HOT,NEW,TOP)

  const handleBadge = (badgeItem) => {
    badge = badgeItem;
    getPost(subreddit, badge);
  };

  // BADGE HANDLE (HOT,NEW,TOP)
</script>

<!-- TITLE -->
<svelte:head>
  <title>Home</title>
</svelte:head>
<!-- TITLE -->

<!-- FORM -->
<form class="form" on:submit|preventDefault={handleSubmit}>
  <!-- <input type="text" bind:value={subreddit} /> -->
  <input
    bind:value={subreddit}
    class="searchfield"
    type="text"
    onkeyup="if(this.value.length > 0) document.getElementById('update-btn').disabled = false; else document.getElementById('update-btn').disabled = true;"
  />
  <input
    id="update-btn"
    type="submit"
    value="Update"
    on:click|preventDefault={handleSubmit}
    disabled
  />
  <div class="trend-badge">
    <li on:click={() => handleBadge("hot")}>Hot</li>
    <li on:click={() => handleBadge("new")}>New</li>
    <li on:click={() => handleBadge("top")}>Top</li>
  </div>
</form>
<!-- FORM -->

<!-- LOADING AND ERROR HANDLING -->
{loading ? "Loading..." : ""}
{isError ? "Subreddit doesn't exist or there was an error" : ""}
<!-- LOADING AND ERROR HANDLING -->

<!-- LOOPING POST FROM API -->
{#each posts as post}
  <PostCard
    title={post.data.title}
    img_url={post.data.url_overridden_by_dest}
  />
  <!-- <PostCard
    img_url="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/gettyimages-912883678-1610452019.jpg?crop=0.6650390625xw:1xh;center,top&resize=640:*"
    title="Test"
  /> -->
{/each}

<!-- LOOPING POST FROM API -->
<style>
  .form {
    display: flex;
    justify-content: center;
    padding: 1em;
  }
  #update-btn {
    cursor: pointer;
    width: 10%;
    margin-right: 20px;
  }
  .searchfield {
    width: 40%;
    padding: 0.3em;
    font-size: 1.2em;
  }
  .trend-badge {
    float: right;
    display: flex;
    color: white;
    width: 50%;
    background: purple;
    align-items: center;
    justify-content: space-evenly;
    list-style-type: none;
    text-align: center;
  }
  .trend-badge li {
    padding: 0.3em;
    width: 100%;
    border: solid 1px white;
    cursor: pointer;
  }
</style>
