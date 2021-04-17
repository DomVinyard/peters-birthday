<script>
  const birthday = {
    month: 4,
    date: 18,
  };
  export let isLoaded;
  export let isToday;
  const checkIsToday = () => {
    const now = new Date();
    isToday =
      now.getMonth() + 1 === birthday.month && now.getDate() === birthday.date;
  };
  checkIsToday();
  $: setInterval(checkIsToday, 10000);

  let src = "./dave.gif";

  function preload(src) {
    return new Promise(function (resolve) {
      let img = new Image();
      img.onload = () => {
        resolve();
        isLoaded = true;
      };
      img.src = src;
    });
  }
</script>

{#await preload(src) then _}
  <main
    class={isToday ? "yes" : "no"}
    style="background-image: url('./dave.gif')"
  >
    <h1>{isToday ? "YES" : "NO"}</h1>
  </main>
{/await}
{#if !isLoaded}
  <main><h1 class="loading">LOADING</h1></main>
{/if}

<style>
  main {
    text-align: center;
    padding: 0em;
    margin: 0;
    height: 100vh;
    width: 100vw;
    justify-content: center;
    align-items: center;
    display: flex;
    background-size: cover;
    background-position: center center;
  }

  .no {
    background-blend-mode: luminosity;
    background-color: rgba(255, 255, 255, 1);
  }

  h1 {
    color: white;
    background: black;
    text-transform: uppercase;
    display: block;
    max-width: 240px;
    font-size: 5em;
    font-weight: 800;
    padding: 0px 32px;
    margin: 0;
  }

  .loading {
    color: black;
    background: white;
    max-width: 440px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
