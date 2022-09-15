<script setup>
import { onMounted } from "vue";

import { db } from "../firebaseInit";
import { query, collection, getDocs, addDoc, doc, getDoc, updateDoc, deleteDoc } from "firebase/firestore";

onMounted(async () => {
  // await writeData();
  await readSingleData("ZzojG7LJF83fjFRFJ9ra");
  await readData();
  // await updateData("wfOasESaGH7TlJagSm6B", "Updated Title!");
  await deleteData("wfOasESaGH7TlJagSm6B");
});

const readData = async () => {
  const docRef = query(collection(db, "questions"));
  try {
    const querySnapshot = await getDocs(docRef);
    querySnapshot.forEach((doc) => {
      console.log(doc.id, doc.data());
    });
  } catch (e) {
    console.error(e);
  }
};

const readSingleData = async (id) => {
  const docRef = doc(db, "questions", id);
  try {
    const docSnap = await getDoc(docRef);
    if (docSnap.exists()) {
      console.log(docSnap.data());
    } else {
      console.log("No such document!");
    }
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

const updateData = async (id, title) => {
  const docRef = doc(db, "questions", id);
  try {
    await updateDoc(docRef, {
      question: title,
    });
    console.log("Document successfully updated!");
  } catch (e) {
    console.error("Error updating document: ", e);
  }
};

const deleteData = async (id) => {
  const docRef = doc(db, "questions", id);
  try {
    await deleteDoc(docRef);
    console.log("Document successfully deleted!");
  } catch (e) {
    console.error("Error removing document: ", e);
  }
};
</script>

<template>
  <h1 class="text-center text-3xl font-bold my-4 text-blue-800">Hello World!</h1>
</template>
