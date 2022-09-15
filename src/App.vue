<script setup>
import { onMounted } from "vue";

import { db } from "../firebaseInit";
import { query, collection, getDocs, addDoc } from "firebase/firestore";

onMounted(async () => {
  await writeData();
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

const writeData = async () => {
  const docRef = await addDoc(collection(db, "questions"), {
    question: "<p></p> 是什麼標籤？",
    answers: [
      { text: "標題", isCorrect: false },
      { text: "段落", isCorrect: true },
      { text: "連結", isCorrect: false },
      { text: "清單", isCorrect: false },
    ],
  });
  console.log("Document written with ID: ", docRef.id);
};
</script>

<template>
  <h1 class="text-center text-3xl font-bold my-4 text-blue-800">Hello World!</h1>
</template>
