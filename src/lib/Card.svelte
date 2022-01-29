<script>
  export let data = {};
  export let i = 1;
</script>

<div class="card" style={`--bg:url(${data.node.main_picture.large})`}>
  <div class="content">
    <h2>" {data.node.title} "</h2>
    <p>ranked</p>
    {#if !i}
      <h3>Number <span>{data.ranking.rank}</span></h3>
    {:else}
      <button id="higher" on:click
        >Higher <svg style="width:24px;height:24px" viewBox="0 0 24 24">
          <path fill="currentColor" d="M7,15L12,10L17,15H7Z" />
        </svg></button
      >
      <button id="lower" on:click
        >Lower<svg style="width:24px;height:24px" viewBox="0 0 24 24">
          <path fill="currentColor" d="M7,10L12,15L17,10H7Z" />
        </svg></button
      >
    {/if}
  </div>
</div>

<style>
  .card {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    background-image: var(--bg);
    background-size: cover;
    background-position: center;
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

  span {
    color: rgb(255, 240, 102);
  }

  @media (max-width: 600px) {
    .card {
      height: 50vh;
    }
  }
</style>
