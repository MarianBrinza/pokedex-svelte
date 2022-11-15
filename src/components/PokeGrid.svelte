<script>
  import PokeCard from "./PokeCard.svelte";

  export let pokemons;
  export let handleCardClicked;

  console.log('rerender')
</script>
<div class="pokeGrid">
  <ul class='center'>
    {#each pokemons as pokemon, index}
      <li>
        <PokeCard
            on:showDetails
            pokemon={pokemon}
            handleCardClicked={handleCardClicked}
        />
      </li>
    {/each}
  </ul>
</div>