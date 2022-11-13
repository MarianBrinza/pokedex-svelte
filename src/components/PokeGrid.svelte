<script>
  import PokeCard from "./PokeCard.svelte";

  export let pokemons;
  export let handleCardClicked;

  console.log('pokemons: ', pokemons);
</script>
<div class="pokeGrid">
  <ul class='center'>
    {#each pokemons as pokemon, index}
      <li>
        <PokeCard
            pokemon={pokemon}
            handleCardClicked={handleCardClicked}
        />
      </li>
    {/each}
  </ul>
</div>