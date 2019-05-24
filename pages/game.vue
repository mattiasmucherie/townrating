<template>
  <section>
    <ul v-for="town in towns" :key="town.id">
      <li>{{town.name}}</li>
    </ul>
  </section>
</template>

<script>
import { fireDb } from "~/plugins/firebase.js";
export default {
  data() {
    return {
      text: "oki",
      towns: []
    };
  },
  async asyncData() {
    const ref = fireDb.collection("towns");
    let snap;
    let listOfTowns = [];
    try {
      let snap = await ref.get();
      snap.forEach(doc => {
        listOfTowns.push(doc.data());
      });
    } catch (e) {
      console.log("error", e.message);
    }
    return {
      towns: listOfTowns
    };
  }
};
</script>

<style>
</style>
