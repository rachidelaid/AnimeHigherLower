<script>
  import Game from './lib/Game.svelte';
  import Start from './lib/Start.svelte';
  import Lose from './lib/Lose.svelte';
  import LeaderBoard from './lib/LeaderBoard.svelte';

  let state = 'start';
  let score = 0;

  const play = (e) => {
    if (e.target.id == 'start') {
      state = 'game';
    } else {
      state = 'board';
    }
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

{#if state === 'board'}
  <LeaderBoard on:click={home} />
{/if}
