<script>
  // svelte curso
  // https://www.youtube.com/watch?v=gjqpEwISXlw&list=PLTd5ehIj0goM-5mQxXLmCr5nHZX_yc2QT&index=18
  // curso fazt con deploy
  // https://www.youtube.com/watch?v=liwD_GPysZs
  import Character from "./lib/Character.svelte";

  let current_page = 1;
  let last_page = null;
  let characters = [];

  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + current_page
    );
    const data = await response.json();
    last_page = data.info.pages;
    characters = data.results;
  }

  loadCharacters();

  function previousPage() {
    current_page--;
    loadCharacters();
  }

  function nextPage() {
    current_page++;
    loadCharacters();
  }
</script>

<h1 class="title">Rick And Morty - Svelte APP</h1>

<div class="container">
  <div class="btns">
    <button class="btn" on:click={previousPage} disabled={current_page === 1}
      >Previous</button
    >
    <button
      class="btn"
      on:click={nextPage}
      disabled={current_page === last_page}>Next</button
    >
  </div>

  <div class="grid">
    {#each characters as char}
      <Character character={char} />
    {/each}
  </div>
</div>
