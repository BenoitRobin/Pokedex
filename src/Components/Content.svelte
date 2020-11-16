<script>
  import Searchbar from "./Searchbar.svelte";

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
          });
      });
  }
</script>

<!-- MON STYLE -->
<style type="text/scss">
  .container {
    max-width: 1400px;
    width: 95%;
    padding: 0 50px;
    margin: 0 auto;

    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
</style>

<!-- MON CODE -->

<Searchbar />
<main class="container">
  Lorem ipsum dolor sit, amet consectetur adipisicing elit. Similique est
  facilis quos sit sequi ea accusamus repellat aliquam minima tempora, quo
  blanditiis assumenda, dolorum vel dolores quisquam officiis eligendi.
  Officiis.
</main>
