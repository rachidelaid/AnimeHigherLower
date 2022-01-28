<script>
  import { onMount } from 'svelte';
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  import Card from './Card.svelte';

  let gameState = 'null';

  let list = [];
  let index = 0;
  let score = 0;

  $: arr = list.slice(index, index + 2);

  onMount(async () => {
    const res = await fetch('./src/list.json');
    const { data } = await res.json();
    list = data.sort(() => Math.random() - 0.5);
  });

  const win = () => {
    setTimeout(() => {
      index = index + 1;
      score = score + 1;
    }, 1000);

    gameState = 'win';
    document.querySelector('.circle').style.setProperty('--winHeight', '100%');
  };

  const handleClick = (e) => {
    if (e.target.id === 'lower') {
      if (arr[0].ranking.rank <= arr[1].ranking.rank) {
        win();
      } else {
        setTimeout(() => {
          dispatch('lost', score);
        }, 1000);

        gameState = 'lose';
        document
          .querySelector('.circle')
          .style.setProperty('--loseHeight', '100%');
      }
    }

    if (e.target.id === 'higher') {
      if (arr[0].ranking.rank >= arr[1].ranking.rank) {
        win();
      } else {
        setTimeout(() => {
          dispatch('lost', score);
        }, 1000);

        gameState = 'lose';
        document
          .querySelector('.circle')
          .style.setProperty('--loseHeight', '100%');
      }
    }
    setTimeout(() => {
      document.querySelector('.circle').style.setProperty('--loseHeight', '0');
      document.querySelector('.circle').style.setProperty('--winHeight', '0');
      gameState = 'null';
    }, 1000);
  };
</script>

<main>
  <div class="game">
    {#each arr as data, i (data.node.id)}
      <Card {data} {i} on:click={handleClick} />
    {/each}
    <div class="check">
      <div class="circle">
        {#if gameState === 'null'}
          <p>VS</p>
        {/if}
        {#if gameState === 'lose'}
          <svg style="width:40px;height:40px" viewBox="0 0 24 24">
            <path
              fill="currentColor"
              d="M20 6.91L17.09 4L12 9.09L6.91 4L4 6.91L9.09 12L4 17.09L6.91 20L12 14.91L17.09 20L20 17.09L14.91 12L20 6.91Z"
            />
          </svg>
        {/if}
        {#if gameState === 'win'}
          <svg style="width:40px;height:40px" viewBox="0 0 24 24">
            <path
              fill="currentColor"
              d="M9,20.42L2.79,14.21L5.62,11.38L9,14.77L18.88,4.88L21.71,7.71L9,20.42Z"
            />
          </svg>
        {/if}
      </div>
    </div>
    <h2>Score: {score}</h2>
  </div>
</main>

<style>
  .game {
    display: flex;
  }

  .check {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-40px, -40px);
  }

  .circle {
    background-color: #fff;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 28px;
    font-weight: bold;
  }

  .circle::before {
    border-radius: 50%;
    background-color: rgb(255, 117, 93);
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: var(--loseHeight, 0);
    content: '';
    transition: all 0.25s ease-in-out;
  }

  .circle::after {
    border-radius: 50%;
    background-color: rgb(112, 255, 93);
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: var(--winHeight, 0);
    content: '';
    transition: all 0.25s ease-in-out;
  }

  .circle p,
  .circle svg {
    z-index: 9;
  }

  h2 {
    position: fixed;
    bottom: 0;
    right: 10px;
    color: #fff;
  }
</style>
