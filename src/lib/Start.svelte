<script>
  // your script goes here
</script>

<div class="start">
  <h3>the</h3>
  <h1>Anime Higher Lower</h1>
  <h3>game</h3>

  <button on:click
    >START<svg style="width:24px;height:24px" viewBox="0 0 24 24">
      <path fill="currentColor" d="M10,17L15,12L10,7V17Z" />
    </svg></button
  >
</div>

<style>
  .start {
    height: 100vh;
    background-color: #111;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  h1 {
    margin: 0;
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
