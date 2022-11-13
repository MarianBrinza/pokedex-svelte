<script>
  export let pokidemonId;
  export let pokemon;
  export let handleCardClicked;

  const {id, img, name} = pokemon;

</script>

<div class="pokeCard" on:click={()=>{handleCardClicked(id)}}>
  <h2>{`#${id.toString().padStart(3, '0')}`}</h2>
  <img src={img} alt={`pokemon ${name}`}/>
  <h2>{name}</h2>
</div>