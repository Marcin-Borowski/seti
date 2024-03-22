<script>
  import Post from "$lib/parts/Post.svelte";

  let count = 0;

  let show = true;

  const add = () => {
    count += 1;
    show = !show;
  };

  const sub = () => {
    count -= 1;
    show = !show;
  };

  let posts = [
    { id: 1, title: "Post 1", body: "This is the body of post 1" },
    { id: 2, title: "Post 2", body: "This is the body of post 2" },
    { id: 3, title: "Post 3", body: "This is the body of post 3" },
    { id: 4, title: "Post 4", body: "This is the body of post 3" },
    { id: 5, title: "Post 5", body: "This is the body of post 3" },
    { id: 6, title: "Post 6", body: "This is the body of post 3" },
    { id: 7, title: "Post 7", body: "This is the body of post 3" },
    { id: 8, title: "Post 8", body: "This is the body of post 3" },
    { id: 9, title: "Post 9", body: "This is the body of post 3" },
    { id: 10, title: "Post 10", body: "This is the body of post 10" },
  ];

  let films = [];

  const getFilms = async () => {
    const base = "https://swapi.dev/api/";
    const url = "films";

    const res = await fetch(base + url);
    const data = await res.json();
    films = data.results;

    console.log(films.stringify());
  };
</script>

<div class="flex container mx-auto text-4xl justify-center items-center gap-4">
  <h1 class="text-center" class:text-red-500={show}>{count}</h1>
  <div>
    {#if show}
      <button on:click={add} class=" bg-red-300"> + </button>
    {:else}
      <button on:click={sub} class=" bg-green-300"> - </button>
    {/if}
  </div>
</div>

<hr />

<div class="container mx-auto">
  <h1 class="text-4xl text-center">Posts</h1>
  <div class="grid grid-cols-4 gap-4">
    {#each posts as post}
      <Post {...post} />
    {/each}
  </div>
</div>

<hr />

<div class="container mx-auto">
  <h1 class="text-4xl text-center">Films</h1>

  <div>
    <button on:click={getFilms}>GET</button>
  </div>

  <div class="grid grid-cols-4 gap-4">
    {#each films as film}
      <div>{film.title}</div>
    {/each}
  </div>
</div>

<style>
  button {
    @apply rounded-md shadow-md border px-3 py-1 text-white border-black;
  }
</style>
