<script setup>
import { onMounted } from "vue";

import { db } from "../firebaseInit";
import { query, collection, getDocs } from "firebase/firestore";
</script>

<template>
  <h1 class="text-center text-3xl font-bold my-4 text-blue-800">Hello World!</h1>
</template>
