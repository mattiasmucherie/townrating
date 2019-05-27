<template>
  <section class="container">
    <div class="headlines">
      <h1 class="title">Är staden en håla eller inte?</h1>
      <n-link to="/game" class="start">STARTA</n-link>
      <n-link to="/addcity" class="addcity">ADD CITY</n-link>
    </div>
  </section>
</template>

<script>
export default {};
</script>


<style lang="scss">
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  max-width: 50vh;
}
.headlines {
  display: block;
  text-decoration: none;
  color: #000;
}
.title {
  font-size: 2rem;
  margin: 32px;
}
.start,
.addcity {
  display: block;
  margin: 16px 32px;
  padding: 16px;
  background: #04724d;
  border-radius: 12px;
  color: #f5f5f9;
  font-weight: bolder;
  text-decoration: none;
  transition: background 0.2s ease;
  border: 4px solid #04724d;
  &:hover {
    background: #f5f5f9;
    color: #04724d;
  }
}
</style>
