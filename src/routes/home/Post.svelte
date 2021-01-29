<script>
  // ALL IMPORTS
  import { onMount } from "svelte";
  import PostCard from "./PostCard.svelte";
  // ALL IMPORTS

  //   VARIABLES AND LISTS
  let posts = [];
  let isError = false;
  let subreddit;
  let loading = true;

  //   VARIABLES AND LISTS

  //   GET REDDIT POSTS
  const getPost = async (subReddit) => {
    try {
      let res = await fetch(
        `https://www.reddit.com/r/${subReddit}/hot.json?limit=40`
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
    getPost("reactjs");
  });
  // ONMOUNT

  //   FORM SUBMIT FUNCTIONS
  const handleSubmit = () => {
    loading = true;
    getPost(subreddit);
    loading = false;
    subreddit = "";
  };
  //   FORM SUBMIT FUNCTIONS
</script>

<!-- TITLE -->
<svelte:head>
  <title>Home</title>
</svelte:head>
<!-- TITLE -->

<!-- FORM -->
<form on:submit|preventDefault={handleSubmit}>
  <input type="text" bind:value={subreddit} />
  <input type="submit" value="Update" on:click|preventDefault={handleSubmit} />
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
{/each}
<!-- LOOPING POST FROM API -->
