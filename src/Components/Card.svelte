<script>
  export let name;
  export let pic;
</script>

<!-- MON STYLE -->
<style type="text/scss">
  .card {
    width: 250px;
    height: 250px;
    background-color: rgba(43, 144, 217, 0.25);
    margin: 2rem;
    border-radius: 10px;
    border: 1px solid #d9e1e8;
    transition: transform 0.3s ease-out;
    -webkit-box-shadow: 9px 8px 0px 0px #9baec8;
    box-shadow: 9px 9px 0px 0px #9baec8;

    display: flex;
    flex-direction: column-reverse;
    justify-content: center;
    align-items: center;
    &-title {
      font-family: "Fredoka One", cursive;
      font-size: 1.3rem;
    }
    &-img {
    }
  }

  .card:hover {
    transform: translate(9px, 9px);
    box-shadow: none;
  }
</style>

<!-- MON CODE -->

<article class="card">
  <p class="card-title">{name}</p>
  <img src={pic} alt={name} class="card-img" />
</article>
