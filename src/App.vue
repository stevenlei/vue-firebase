<script setup>
import { onMounted } from "vue";

import { db } from "../firebaseInit";
import { query, collection, getDocs } from "firebase/firestore";

onMounted(async () => {
  await readData();
});

const readData = async () => {
  const ref = query(collection(db, "questions"));
  try {
    const querySnapshot = await getDocs(ref);
    querySnapshot.forEach((doc) => {
      console.log(doc.id, doc.data());
    });
  } catch (e) {
    console.error(e);
  }
};
</script>

<template>
  <h1 class="text-center text-3xl font-bold my-4 text-blue-800">Hello World!</h1>
</template>
