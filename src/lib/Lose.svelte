<script>
  import { onMount } from 'svelte';

  export let score;

  let img;
  let show = false;

  onMount(async () => {
    const res = await fetch(
      'https://g.tenor.com/v1/search?q=lose&key=SJICIPYYIQ2D',
    );
    const { results } = await res.json();
    img = results[Math.floor(Math.random() * 20)].media[0].gif.url;
  });

  const showInput = (e) => {
    if (show && e.target.id === 'modal') {
      show = false;
      return;
    }

    show = true;
  };

  const submit = (e) => {
    show = false;
    const obj = {
      user: e.target.elements.username.value.trim(),
      score,
    };
    fetch(
      'https://us-central1-js-capstone-backend.cloudfunctions.net/api/games/7KnK7q73461Vs7VjieM2/scores',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(obj),
      },
    );

    e.target.reset();
  };
</script>

<div class="retray" style={`--bg:url(${img})`}>
  <div class="content">
    <h3>Your Score:</h3>
    <h1>{score}</h1>
    <div class="btns">
      <button on:click={showInput}>SAVE SCORE</button>
      <button on:click>HOME</button>
    </div>
  </div>

  {#if show}
    <div class="modal" id="modal" on:click={showInput}>
      <form on:submit|preventDefault={submit}>
        <input type="text" id="username" placeholder="Your Name" required />
        <button type="submit">SUBMIT</button>
      </form>
    </div>
  {/if}
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

  .btns {
    display: flex;
    gap: 50px;
  }

  h1 {
    color: rgb(255, 240, 102);
  }

  .modal {
    position: fixed;
    left: 0;
    top: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.9);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  form {
    padding: 20px;
    width: 70%;
    background-color: #222;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  form input {
    width: 100%;
    background-color: transparent;
    padding: 10px;
    border-radius: 10px;
    color: #fff;
    font-size: 18px;
    border: 2px solid #fff;
  }
</style>
