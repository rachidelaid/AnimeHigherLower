<script>
  import { onMount } from 'svelte';

  let list = [];

  onMount(async () => {
    const res = await fetch(
      'https://us-central1-js-capstone-backend.cloudfunctions.net/api/games/7KnK7q73461Vs7VjieM2/scores',
    );
    const { result } = await res.json();
    list = result.sort((a, b) => b.score - a.score);
  });
</script>

<div class="container">
  <h2>Leader Board:</h2>
  <button on:click>Back</button>
  <ul>
    {#if !list.length}
      <li>No Scores Yet!</li>
    {:else}
      {#each list as item, index (index)}
        <li>
          {#if index < 3}
            <svg viewBox="0 0 24 24">
              <path
                fill="currentColor"
                d="M12,17.27L18.18,21L16.54,13.97L22,9.24L14.81,8.62L12,2L9.19,8.62L2,9.24L7.45,13.97L5.82,21L12,17.27Z"
              />
            </svg>
          {/if}
          {item.user}: {item.score}
        </li>
      {/each}
    {/if}
  </ul>
</div>

<style>
  .container {
    height: 100vh;
    background-color: #111;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 0 20px;
  }

  h2 {
    margin: 0;
  }

  button {
    margin: 10px 0;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    width: 100%;
    max-height: 70%;
    overflow: auto;
  }

  li {
    padding: 10px;
    background-color: #000;
    display: flex;
    align-items: center;
    gap: 10px;
    padding-left: 50px;
  }

  li:nth-child(even) {
    background-color: #333;
  }

  li:nth-child(1) {
    padding: 10px;
  }
  li:nth-child(2) {
    padding: 10px;
  }
  li:nth-child(3) {
    padding: 10px;
  }

  svg {
    width: 30px;
  }

  li:nth-child(1) svg {
    color: rgb(255, 213, 25);
  }
  li:nth-child(2) svg {
    color: rgb(179, 179, 179);
  }
  li:nth-child(3) svg {
    color: rgb(212, 101, 37);
  }
</style>
