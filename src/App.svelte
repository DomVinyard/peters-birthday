<script>
  const birthday = {
    month: 4,
    date: 17,
  };
  export let isToday;
  const checkIsToday = () => {
    const now = new Date();
    isToday =
      now.getMonth() + 1 === birthday.month && now.getDate() === birthday.date;
  };
  checkIsToday();
  $: setInterval(checkIsToday, 10000);
</script>

<main style="background-image: url('./dave.gif')">
  <h1>{isToday ? "YES" : "NO"}</h1>
</main>

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

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
