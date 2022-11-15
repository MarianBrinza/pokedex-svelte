<script>
  import {afterUpdate, onMount} from "svelte";
  import {colors, pokeDetails} from "../utils/constants";
  import {getPokemonDetails} from "../utils/util";

  export let selectedPokemonId;
  let details;

  onMount(() => {
    if (!selectedPokemonId) return;

    fetch(`${pokeDetails}${selectedPokemonId}`)
      .then(res => res.json())
      .then(data => {
        const pokemonDetails = getPokemonDetails(data);
        details = pokemonDetails;
      });
  });

  afterUpdate(() => {
    console.log(1)
    if (selectedPokemonId) {
      console.log(2)
      let ul = document.querySelector('ul.center');
      const ulWidth = ul.offsetWidth;
      if (ulWidth > 1000) return;
      console.log(3)
      ul.style.width = `${ulWidth}px`;
    }
  });

</script>

{#if details}

  <div class="pokeDetails">

    <div class="detailsContainer">
      <div class="detailsImgContainer">
        <img src={details.img} alt={`pokemon ${details.name}`}/>
      </div>

      <div class="statsContainer">
        <h2>{details.name}</h2>
        <hr class='separator' style="border-color: {colors[details.type[0]]}"/>
        <h3>{details.id}</h3>

        <p>Type:
          {#each details.type as type}
            <span class='pokeType' style="background: {colors[type]}">{type} </span>
          {/each}
        </p>

        <p>Weight: <span class='weight'>{details.weight} kg</span></p>
        <p>Height: <span class='height'>{details.height} m</span></p>

        <p>Skills:
          {#each details.abilities as ability}
            <span class='ability'> 💥{ability}</span>
          {/each}
        </p>

        <div class="stats">
          <div class="hp">
            <h4>Hit Points <span class='emojy heart'>❤</span></h4>
            <span>{details.stats.hp}/399</span>
          </div>
          <div class="attack">
            <h4>Attack <span class='emojy sword'>⚔</span></h4>
            {details.stats.attack}/345
          </div>
          <div class="defense">
            <h4>Defense <span class='emojy shield'>🛡</span></h4>
            {details.stats.defense}/396
          </div>
        </div>
      </div>

    </div>
  </div>
{/if}