<template>
  <section class="container">
    <div class="containerTitles">
      <h1>{{town.name}}</h1>
      <h2>{{town.county}}</h2>
      <h2>{{town.population}}</h2>
    </div>
  </section>
</template>

<script>
import { fireDb } from "~/plugins/firebase.js";
import firebase from "firebase/app";
export default {
  data() {
    return {};
  },
  async asyncData() {
    const ref = fireDb.collection("towns");
    const key = ref.doc().id;
    let town = null;

    try {
      const snap = await ref
        .where(firebase.firestore.FieldPath.documentId(), ">=", key)
        .limit(1)
        .get();
      if (snap.size > 0) {
        snap.forEach(doc => {
          town = doc.data();
          town.id = doc.id;
        });
      } else {
        const snap2 = await ref
          .where(firebase.firestore.FieldPath.documentId(), "<=", key)
          .limit(1)
          .get();
        snap2.forEach(doc => {
          town = doc.data();
          town.id = doc.id;
        });
      }
    } catch (err) {
      //TODO: handle errors
      console.log(err);
    }
    return {
      town
    };
  }
};
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
.containerTitles {
  display: block;
}
</style>
