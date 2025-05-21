<script setup>
import { ref, onMounted } from "vue";

const count = ref(0);
const increaseCouunter = () => {
  count.value += 1;
};

defineProps({
  messageText: String,
  changeMessage: Function,
});

onMounted(() => {
  console.log("on mouted at Counter.vue")
});
</script>

<template>
  <div>Hello {{ messageText }}</div>
  <div>
    <input type="text" v-model="message" /><br />
    <button @click="changeMessage(message)">Change message from counter</button>
  </div>
  <button @click="increaseCouunter">Click {{ count }}</button>
</template>
