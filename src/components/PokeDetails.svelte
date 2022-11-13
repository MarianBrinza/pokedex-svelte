<script>
  import {colors, pokeDetails} from "../utils/constants";
  import {onMount} from "svelte";

  export let selectedPokemonId;
  let details = {};

  console.log('selectedPokemonId: ', selectedPokemonId)

  onMount( async () => {
    if (!selectedPokemonId) return;
    const response = await fetch(`${pokeDetails}${selectedPokemonId}`);
    console.log('respinse: ', response);
  });

</script>

<div class="pokeDetails">

  <div class="detailsContainer">
    <div class="detailsImgContainer">
      <img src={details.img} alt={`pokemon ${details.name}`}/>
    </div>


    <div class="statsContainer">
      <h2>{details.name}</h2>
      <hr class='separator' style={{borderColor: primaryType}}/>
      <h3>{details.id}</h3>
      <p>Type:
        <!--{-->
        <!--  details.type.map(type => {-->
        <!--    const color = colors[type];-->
        <!--    return <span class='pokeType' style={{background: color}}>{type} </span>-->
        <!--  })-->
        <!--}-->
      </p>

      <p>Weight: <span class='weight'>{details.weight} kg</span></p>
      <p>Height: <span class='height'>{details.height} m</span></p>

      <p>Skills:
        <!--{-->
        <!--  details.abilities.map(ability => {-->
        <!--    return <span class='ability'> 💥{ability}</span>-->
        <!--  })-->
        <!--}-->
      </p>

      <div class="stats">
        <div class="hp">
          <h4>Hit Points <span class='emojy heart'>❤</span></h4>
          {details.stats.hp}/399
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