
<template>
  <div class="container">
    <div class="form-container">
      <form class="submission-form" name="addtown" v-on:submit.prevent="addTown">
        <h1 class="title">Add a City</h1>
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
      population: null
    };
  },
  methods: {
    async addTown() {
      const ref = fireDb.collection("towns");
      const body = {
        county: this.county,
        name: this.name,
        population: Number(this.population),
        rating: { negative: 0, positive: 0 }
      };
      let response;
      try {
        response = await ref.add(body);
        console.log(response);
        this.name = "";
        this.county = "";
        this.population = null;
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
    border: 2px solid #fff;
    &:focus {
      border: 2px solid #b8dbd9;
    }
  }
  .form-button {
    display: block;
    border: 0;
    background: #b8dbd9;
    width: auto;
    margin: 1rem auto;
    padding: 8px;
    text-transform: uppercase;
    color: #000;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background 0.2s ease;
    border: 4px solid #b8dbd9;
    &:hover {
      background: #586f7c;
      color: #f5f5f9;
    }
  }
}
.form-container {
  background: #586f7c;
  border-radius: 1rem;
  color: #f5f5f9;
}
</style>
