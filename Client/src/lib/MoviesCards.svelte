<script>
  export let value;
  import { debounce } from "../utils/debounce";

  let response = [];

  const handleSearch = debounce(async () => {
    if (value.length > 1) {
      response = fetch(`https://omdbapi.com/?apikey=11a59b1e&s=${value}`)
        .then((res) =>
          !res.ok ? new Error("Something bad happened") : res.json(),
        )
        .then((data) => data.Search || []);
    }
  }, 400);

  $: handleSearch(value);

  $: {
    console.log("response", response);
  }
</script>

{#await response}
  <strong class="textR">Loading...</strong>
{:then movies}
  <ul class="moviesCards">
    {#each movies as movie}
      <li class="movieCard">
        <img
          class="image"
          src={movie.Poster}
          alt={`${movie.Title} minature img`}
        />
        <div class="type">
          <small>{movie.Type.toLocaleUpperCase()}</small>
        </div>
        <div class="infoPanel">
          <strong class="">{movie.Title}</strong>
        </div>
      </li>
    {:else}
      {#if value.length < 1}
        <strong class="textR">Search in for a movie!</strong>
      {:else}
        <strong class="textR">Nothing was found</strong>
      {/if}
    {/each}
  </ul>
{:catch error}
  <span>There has been an error {error}</span>
{/await}

<style>
  .textR {
    font-size: 1.5rem
  }
  .moviesCards {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    row-gap: 40px;
    column-gap: 20px;
    list-style: none;
    justify-content: space-around;
    
    padding: 0px;
  }
  .movieCard {
    display: flex;
    flex-direction: column;
    border: 1px solid rgb(53, 122, 150);
    object-fit: cover;
    position: relative;
    overflow: hidden;
    justify-content: flex-start;
    align-items: start;
    align-self: start;
  }
  .image {
    object-fit: fill;
    display: flex;
    min-width: 18rem;
    max-width: 18rem;
    min-height: 25rem;
    max-height: 25rem;
  }
  .infoPanel {
    position: absolute;
    bottom: 0;
    z-index: 50;
    background-color: rgb(27, 53, 63);
    justify-content: start;
    display: flex;
    width: 100%;
    padding: 10px 10px 10px 10px;
    font-size: 1rem;
  }
  .type {
    position: absolute;
    top: 0;
    right: 0;
    z-index: 50;
    background-color: rgb(27, 53, 63);
    justify-content: start;
    display: flex;
    width: fit-content;
    padding: 5px 10px 5px 10px;
  }
</style>
