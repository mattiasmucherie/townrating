<template>
  <section>
    <h1>{{town}}</h1>
  </section>
</template>

<script>
import { fireDb } from "~/plugins/firebase.js";
import firebase from "firebase/app";
export default {
  data() {
    return {
      town: "null"
    };
  },
  async asyncData() {
    const ref = fireDb.collection("towns");
    var key = ref.doc().id;

    console.log(key);
    ref
      .where(firebase.firestore.FieldPath.documentId(), ">=", key)
      .limit(1)
      .get()
      .then(snapshot => {
        if (snapshot.size > 0) {
          snapshot.forEach(doc => {
            console.log(doc.id, "=>", doc.data());
          });
        } else {
          const quote = ref
            .where(firebase.firestore.FieldPath.documentId(), "<=", key)
            .limit(1)
            .get()
            .then(snapshot => {
              snapshot.forEach(doc => {
                console.log(doc.id, "=>", doc.data());
              });
            })
            .catch(err => {
              console.log(err);
            });
        }
      })
      .catch(err => {
        console.log(err);
      });
    return {
      town: { name: "Nyköping" }
    };
  }
};
</script>

<style>
</style>
