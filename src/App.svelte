<script>1
  import {fade} from "svelte/transition";
  import Layout from "./components/Layout.svelte";
  import PokeGrid from "./components/PokeGrid.svelte";
import {onMount, tick} from "svelte";
  import {pokeApi} from "./utils/constants";
  import {fetchPokemonsInfo, setCssClasses} from "./utils/util";
  import PokeDetails from "./components/PokeDetails.svelte";

  let pokemons = [];
  let selectedPokemonId = null;

  onMount(async () => {
    const response = await fetch(pokeApi);
    const data = await response.json();
    const pokemonInfo = fetchPokemonsInfo(data.results);
    pokemons = pokemonInfo;
  });

  const handleCardClicked = (id) => {
    if (selectedPokemonId === id) return;
    selectedPokemonId = id;
    setCssClasses();
  }

  function handleShowDetails(id) {
    selectedPokemonId = id.detail;
  }

</script>

<main class="app" in:fade>
  <Layout>
    {#if pokemons.length > 0 }
      <PokeGrid pokemons={pokemons} handleCardClicked={handleCardClicked} on:showDetails={handleShowDetails}/>
    {/if}

    <!--{#if selectedPokemonId !== null}-->
    <!--  <PokeDetails selectedPokemonId={selectedPokemonId}/>-->
    <!--{/if}-->

    {#key selectedPokemonId}
        <PokeDetails selectedPokemonId={selectedPokemonId}/>
    {/key}
  </Layout>

</main>
