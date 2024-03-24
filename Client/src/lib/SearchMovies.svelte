<script>
  import MoviesCards from "./MoviesCards.svelte";
  import SearchInput from "./SearchInput.svelte";

  let value = "";
  $: {
    console.log("asara", value);
  }
</script>

<article class="mainContainer">
  <header class="header">
    <h1 class="title">Movies</h1>
    <SearchInput bind:value />
  </header>

  <section
    style="
  justify-content: center; 
  text-align: center; 
  margin-top: 20px;"
  >
    <MoviesCards {value} />
  </section>
</article>

<style>
  .mainContainer {
    font-size: 0.9rem;
    display: flex;
    flex-direction: column;
  }
  .title {
    color: rgb(53, 122, 150);
  }
  .header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    border-bottom: 1px solid rgb(53, 122, 150);
    align-items: center;
    text-align: start;
  }
</style>
