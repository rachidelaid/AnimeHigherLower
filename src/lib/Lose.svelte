<script>
  import { onMount } from 'svelte';

  export let score;

  let img;

  onMount(async () => {
    const res = await fetch(
      'https://g.tenor.com/v1/search?q=lose&key=SJICIPYYIQ2D',
    );
    const { results } = await res.json();
    img = results[Math.floor(Math.random() * 20)].media[0].gif.url;
  });
</script>

<div class="retray" style={`--bg:url(${img})`}>
  <div class="content">
    <h3>Your Score:</h3>
    <h1>{score}</h1>
    <button on:click>HOME</button>
  </div>
</div>

<style>
  .retray {
    height: 100vh;
    background-color: #111;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: var(--bg);
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }

  .content {
    padding: 0 20px;
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.7);
    color: #fff;
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
