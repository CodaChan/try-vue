<script setup lang="ts">
import { ref } from "vue";

// const violet = ref("violet");
const blod = ref("blod");
const isViolet = ref(false);
</script>

<template>
  <p><span :class="[{ violet: isViolet }, blod]">ClassBind</span></p>
</template>

<style>
.violet {
  color: blueviolet;
}

.blod {
  font-weight: bolder;
}
</style>
