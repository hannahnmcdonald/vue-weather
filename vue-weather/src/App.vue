<!-- Markup -->
<template>
  <div id='app'>
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder=" City Search" />
      </div>
    </main>
  </div>
</template>

<script>
// JS Code //

  export default {
    name: 'App',
    data () {
      return {
        api_key: 'c6c69e1807c116c6d2751b910241be75'
      }
    }

  }
</script>

<style>
/* CSS */
  * {
    margin: 0;
    padding: 0;
    box-size: border-box;
  }
  body {
    font-family: 'monserrat', sans-serif;
  }
  #app {
    background-image: url('./assets/bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }
  main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.35));
  }
  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }
  .search-box .search-bar {
    display: block;
    margin: auto;
    margin-top: 2rem;
    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    border: none;
    outline: none;
    background: none;
    box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }
  .search-box .search-bar:focus {
    background-color: rgba(255,255,255,0.75);
  }
</style>
