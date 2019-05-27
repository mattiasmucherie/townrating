<template>
  <section class="container">
    <div class="headlines">
      <h1>Är staden en håla eller inte?</h1>
      <n-link to="/game">STARTA</n-link>
      <n-link to="/addcity">ADD CITY</n-link>
    </div>
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
.headlines {
  display: block;
  text-decoration: none;
  color: #000;
}
</style>
