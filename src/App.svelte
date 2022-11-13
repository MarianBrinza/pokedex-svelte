<script>
  import Layout from "./components/Layout.svelte";
  import PokeGrid from "./components/PokeGrid.svelte";
  import PokeDetails from "./components/PokeDetails.svelte";
  import {onMount} from "svelte";
  import {pokeApi} from "./utils/constants";
  import {fetchPokemonsInfo, setCssClasses} from "./utils/util";

  let pokemons = [];
  let selectedPokemonId = null;

  onMount(async () => {
    const response = await fetch(pokeApi);
    const data = await response.json();
    const pokemonInfo = fetchPokemonsInfo(data.results);
    console.log(pokemonInfo)
    pokemons = pokemonInfo;
  });

  const handleCardClicked = (id) => {
    console.log('cardClicked, ', id);
    if (selectedPokemonId === id) return;
    selectedPokemonId = id;
    console.log({selectedPokemonId, id})
    setCssClasses();
  }

</script>

<main class="app">
  <Layout>
    {#if pokemons.length > 0 }
      <PokeGrid pokemons={pokemons} handleCardClicked={handleCardClicked}/>
    {/if}
    {#if selectedPokemonId !== null}
      <PokeDetails/>
    {/if}
    <!--{#each pokemons as pokemon (pokemon)}-->
    <!--  <h3>{pokemon.name}</h3>-->
    <!--{/each}-->
    <!--<h3>bla</h3>-->
  </Layout>

</main>
