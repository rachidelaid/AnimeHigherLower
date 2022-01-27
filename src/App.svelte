<script>
  import Game from './lib/Game.svelte';
  import Start from './lib/Start.svelte';
  import Lose from './lib/Lose.svelte';

  let state = 'start';
  let score = 0;

  const play = () => {
    state = 'game';
  };

  const home = () => {
    state = 'start';
  };

  const handleLost = (e) => {
    score = e.detail;
    state = 'lose';
  };
</script>

{#if state === 'start'}
  <Start on:click={play} />
{/if}

{#if state === 'game'}
  <Game on:lost={handleLost} />
{/if}

{#if state === 'lose'}
  <Lose {score} on:click={home} />
{/if}

<style>
  /* your styles go here */
</style>
