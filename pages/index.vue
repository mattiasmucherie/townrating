<template>
  <section class="container">
    <h1>Är staden en håla eller inte?</h1>
    <n-link to="/game">STARTA</n-link>
    <n-link to="/addcity">ADD CITY</n-link>
  </section>
</template>

<script>
export default {};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.starta {
  display: inline-block;
  text-decoration: none;
}
</style>
