<script>
  import { onMount } from 'svelte';

  export let score;

  let img;

  onMount(async () => {
    const res = await fetch(
      'https://g.tenor.com/v1/search?q=lose&key=SJICIPYYIQ2D',
    );
    const { results } = await res.json();
    img = results[0].media.gif.url;
  });
</script>

<div class="retray" style={`--bg:url(${img})`}>
  <h3>Your Score:</h3>
  <h1>{score}</h1>
  <button on:click>HOME</button>
</div>

<style>
  .retray {
    height: 100vh;
    background-color: #111;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-image: var(--bg);
    background-size: cover;
    background-position: center;
  }

  h1 {
    color: rgb(255, 240, 102);
  }

  button {
    margin: 5px 0;
    padding: 10px 25px;
    border: 2px solid #fff;
    background-color: transparent;
    display: flex;
    align-items: center;
    gap: 20px;
    font-weight: bold;
    font-size: 18px;
    color: #fff;
    border-radius: 30px;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
  }

  button:hover {
    color: #000;
    background-color: #fff;
  }
</style>
