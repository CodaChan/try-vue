<script setup lang="ts">
import { nextTick, reactive, ref } from "vue";

const rawHtml = ref("<span style='color: red'>Red Text</span>");

const violet = ref("violet");

const msg = ref("hi!!!!!");
const changeMsg = () => {
  if (msg.value === "hi!!!!!") msg.value = "hello!";
  else msg.value = "hi!!!!!";
};
const isButtonDisabled = ref(false);
const lockButtonText = ref("Lock");
const disableButton = () => {
  if (isButtonDisabled.value === false) {
    isButtonDisabled.value = true;
    lockButtonText.value = "Unlock";
  } else {
    isButtonDisabled.value = false;
    lockButtonText.value = "Lock";
  }
};

const objectOfAttrs = {
  id: "violet",
  class: "bold",
};

const getMsg = () => {
  return "Violet" + " " + "Text";
};

const isMsgShow = ref(true);
const hideButtonText = ref("Hide");
const hideButton = () => {
  if (isMsgShow.value === true) {
    isMsgShow.value = false;
    hideButtonText.value = "Show";
  } else {
    isMsgShow.value = true;
    hideButtonText.value = "Hide";
  }
};

const attributeKey = ref("href");
const attributeValue = ref("https://bytedance.com");
const byteStyle = ref("Inspire Objectives, Enrich Key Results!");

const counter = ref(0);
const increment = () => {
  counter.value++;
  console.log("Unsync " + document.querySelector("#plusButton")?.innerHTML);
  nextTick(() => {
    console.log("Sync " + document.querySelector("#plusButton")?.innerHTML);
  });
};

const raw = 0;
const proxy = ref(raw);
proxy.value = 1;
const proxy2 = ref(raw);

const refCounter = {
  count: ref(0),
};
const n = refCounter.count;
const plusRefButton = () => {
  n.value++;
};

const object = {
  foo: ref(0),
};
const { foo } = object;
const reactiveObj = reactive({
  foo: ref(0),
});
const map = new Map([["foo", ref(0)]]);
</script>

<template>
  <h2>Template Syntax</h2>

  <p>raw: {{ rawHtml }}</p>

  <p>
    v-html:
    <span v-html="rawHtml"></span>
  </p>

  <p>
    v-bind:
    <span :id="violet">Violet Text</span>
  </p>

  <p>
    v-on: {{ msg }}
    <button @click="changeMsg" :disabled="isButtonDisabled">Change</button>
    <button @click="disableButton">{{ lockButtonText }}</button>
  </p>

  <p>
    multi v-bind:
    <span v-bind="objectOfAttrs">Bold Violet Text</span>
  </p>

  <p>
    expression:
    <span :id="'vio' + 'let'">{{ getMsg() }}</span>
  </p>

  <p>
    <button @click="hideButton">{{ hideButtonText }}</button>
    <span v-if="isMsgShow"> See me!</span>
  </p>

  <p>
    <a :[attributeKey]="attributeValue">{{ byteStyle }}</a>
  </p>

  <h2>Reactivity Fundamentals</h2>

  <p>
    <button id="plusButton" @click="increment">Count is {{ counter }}</button>
    <span> See console~</span>
  </p>

  <p>
    ref proxy:
    <span>{{ raw }} {{ proxy }} {{ proxy2 }}</span>
  </p>

  <p>
    ref change:
    <button @click="plusRefButton">Count is {{ refCounter.count }}</button>
  </p>

  <p>
    auto unpkg:
    {{ object.foo.value + 1 }} {{ foo + 1 }} {{ object.foo }}
    {{ reactiveObj.foo + 1 }} {{ map.get("foo")?.value }}
  </p>
</template>

<style>
#violet {
  color: blueviolet;
}

.bold {
  font-weight: bolder;
}
</style>
