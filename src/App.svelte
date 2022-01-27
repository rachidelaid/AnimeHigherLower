<script>
  import { onMount } from 'svelte';

  import Card from './lib/Card.svelte';

  let list = [];
  let index = 0;

  onMount(async () => {
    const res = await fetch('./list.json');
    const { data } = await res.json();
    list = data.sort(() => Math.random() - 0.5);
  });
</script>

<main>
  <div class="game">
    {#each list.slice(index, index + 2) as data, i (data.node.id)}
      <Card {data} {i} />
    {/each}
    <div class="check">
      <div class="circle">VS</div>
    </div>
  </div>
</main>

<style>
  main {
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  }

  .game {
    display: flex;
  }

  .check {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-25px, -25px);
  }

  .circle {
    background-color: rgba(255, 255, 255, 0.5);
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
