<script>
  import Searchbar from "./Searchbar.svelte";
  import Card from "./Card.svelte";
  import { v4 as uuidv4 } from "uuid";

  let allPokemon = [];
  let tableauFin = [];

  function fetchPokemonBase() {
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
      .then((res) => res.json())
      .then(function (allPoke) {
        // console.log(allPoke);
        allPoke.results.forEach(function (pokemon) {
          fetchPokemonComplet(pokemon);
        });
      });
  }

  fetchPokemonBase();

  function fetchPokemonComplet(pokemon) {
    let objetPokemonFull = {};
    let url = pokemon.url;
    let namePokemon = pokemon.name;

    fetch(url)
      .then((res) => res.json())
      .then(function (pokeData) {
        objetPokemonFull.pic = pokeData.sprites.back_default;
        fetch(`https://pokeapi.co/api/v2/pokemon-species/${namePokemon}`)
          .then((res) => res.json())
          .then(function (pokeData) {
            // console.log(pokeData);
            objetPokemonFull.name = pokeData.names[4].name;

            allPokemon.push(objetPokemonFull);
            tableauFin = allPokemon.slice(0, 20);
            allPokemon = allPokemon;
          });
      });
  }

  function goRecherche(event) {
    // console.log(event.detail.txt);
    let contenuResearch = event.detail.txt;
    tableauFin = allPokemon.filter((el) => el.name.includes(contenuResearch));
  }
</script>

<!-- MON STYLE -->
<style type="text/scss">
  .scroll-container {
    overflow: scroll;
  }
  .container {
    max-width: 1400px;
    height: 45vh;
    width: 85%;
    margin: 0 auto;
    background-color: #fff;
    box-shadow: inset 5px 5px 6px 0px #2b90d9;

    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    border-radius: 10px;
  }
</style>

<!-- MON CODE -->

<Searchbar on:recherche-pokemon={goRecherche} />

<main class="container scroll-container">
  {#each tableauFin as pokemon (uuidv4())}
    <Card name={pokemon.name} pic={pokemon.pic} />
  {/each}
</main>
