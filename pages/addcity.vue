
<template>
  <div class="container">
    <div class="form-container">
      <form class="submission-form" name="addtown" v-on:submit.prevent="addTown">
        <h1 class="title">Contact</h1>
        <label class="form-label" for="name">Name:</label>
        <input class="form-field" name="name" id="name" v-model="name" type="text" required>
        <label class="form-label" for="county">County</label>
        <input class="form-field" name="county" id="county" v-model="county" type="text" required>
        <label class="form-label" for="population">Population</label>
        <input
          class="form-field"
          name="population"
          id="population"
          v-model="population"
          type="number"
          required
        >
        <label class="form-label" for="population">ID</label>
        <input class="form-field" name="id" id="id" v-model="id" type="number" required>
        <button class="form-button" type="submit" value="Add City">Send</button>
      </form>
    </div>
  </div>
</template>

<script>
import { fireDb } from "~/plugins/firebase.js";

export default {
  data() {
    return {
      name: "",
      county: "",
      population: null,
      id: null
    };
  },
  methods: {
    async addTown() {
      const ref = fireDb.collection("towns");
      const body = {
        county: this.county,
        name: this.name,
        population: Number(this.population),
        id: Number(this.id),
        rating: { negative: 0, positive: 0 }
      };
      let response;
      try {
        response = await ref.add(body);
        console.log(response);
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style lang="scss">
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: #000;
}

.submission-form {
  max-width: 500px;
  margin: 1rem auto;
  padding: 2rem;
  .form-label,
  .form-field {
    display: block;
    width: 100%;
    padding: 0.5rem;
    text-align: left;
    border: none;
    border-radius: 0.3rem;
  }
  .form-field {
    background: #ffffff;
    transition: all 0.2s ease-in-out;
    -webkit-transition: all 0.2s ease-in-out;
    -moz-transition: all 0.2s ease-in-out;
    -ms-transition: all 0.2s ease-in-out;
    -o-transition: all 0.2s ease-in-out;
    border: 1px solid #fff;
    &:focus {
      border: 1px solid #304ffe;
    }
  }
  .form-button {
    display: block;
    border: 0;
    background: #304ffe;
    width: auto;
    margin: 1rem auto;
    padding: 8px;
    text-transform: uppercase;
    color: #fff;
    border-radius: 0.5rem;
    cursor: pointer;
    &:hover {
      background: #0026ca;
      color: #fff;
    }
  }
}
.form-container {
  background: #00b7d3;
  border-radius: 0.2rem;
}
</style>
