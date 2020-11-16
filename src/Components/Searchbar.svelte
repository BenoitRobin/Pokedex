<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let recherche = "";

  function rechercheFunc() {
    // console.log(recherche);
    dispatch("recherche-pokemon", { txt: recherche });
    recherche = "";
  }
</script>

<!-- MON STYLE -->
<style type="text/scss">
  .form-search {
    margin: 10rem auto 4rem auto;
    max-width: 1100px;
    width: 100%;
    padding: 0 50px;

    display: flex;
    flex-direction: column;
    position: relative;
    & label {
      font-size: 2rem;
      font-weight: 500;
      padding-bottom: 1rem;
    }

    & input {
      font-size: 1.6rem;
      padding: 1rem;
      font-weight: 300;
      font-style: italic;
      color: #9baec8;
      border: 1px solid #d9e1e8;
      border-radius: 5px;
      -webkit-box-shadow: 9px 8px 0px 0px #2b90d9;
      box-shadow: 6px 5px 0px 0px #2b90d9;
    }

    & button {
      cursor: pointer;
      width: fit-content;
      margin: 1.5rem auto;
      padding: 1rem 1.5rem;
      font-size: 1.2rem;
      font-family: "Fredoka One", cursive;

      border: 1px solid #d9e1e8;
      border-radius: 5px;
      -webkit-box-shadow: 9px 8px 0px 0px #2b90d9;
      box-shadow: 6px 5px 0px 0px #2b90d9;
    }

    & button:hover {
      transform: translate(6px, 5px);
      box-shadow: none;
    }
  }

  .form-search input,
  .form-search label {
    max-width: 1100px;
    width: 100%;
  }
</style>

<!-- MON CODE -->

<form class="form-search" on:submit|preventDefault={rechercheFunc}>
  <label for="recherche">Cherchez un pokémon :</label>
  <input
    bind:value={recherche}
    type="text"
    id="recherche"
    placeholder="Recherchez votre pokémon..." />
  <button type="submit">Envoyer</button>
</form>
