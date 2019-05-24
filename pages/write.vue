<template>
  <section class="container">
    <div>
      <h2>Write to Firestore.</h2>
      <div>
        <button @click="writeToFirestore" :disabled="writeSuccessful">
          <span v-if="!writeSuccessful">Write now</span>
          <span v-else>Successful!</span>
        </button>
      </div>
    </div>
    <div>
      <h2>Read from Firestore.</h2>
      <div>
        <p>{{text}}</p>
      </div>
    </div>
  </section>
</template>

<script>
import { fireDb } from "~/plugins/firebase.js";
export default {
  data() {
    return {
      writeSuccessful: false,
      readSuccessful: false,
      text: ""
    };
  },
  async asyncData() {
    const ref = fireDb.collection("towns");
    let snap;
    let town;
    try {
      let snap = await ref.get();
      snap.forEach(doc => {
        console.log(doc.id, "=>", doc.data());
        town = doc.data().name;
      });
    } catch (e) {
      console.log(e);
    }
    return {
      text: town
    };
  },
  methods: {
    async writeToFirestore() {
      const ref = fireDb.collection("test").doc("test2");
      const document = {
        text: "This is a test message."
      };

      try {
        await ref.set(document);
      } catch (e) {
        // TODO: error handling
        console.error(e);
      }
      this.writeSuccessful = true;
    },
    async readFromFirestore() {
      const ref = fireDb.collection("test").doc("test2");
      let snap;
      try {
        snap = await ref.get();
      } catch (e) {
        // TODO: error handling
        console.error(e);
      }
      this.text = snap.data().text;
      this.readSuccessful = true;
    }
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
