<script setup>
import { ref, reactive, watch, watchEffect } from "vue";

const formData = reactive({
  firstname: "",
  lastname: "",
});

const fullname = ref("");

watchEffect(() => {
    fullname.value = `${formData.firstname} ${formData.lastname}`;
  }
);
</script>

<template>
  <div>
    <div>Fullname : {{ fullname }}</div>
    <input type="text" v-model="formData.firstname" /> <br />
    <input type="text" v-model="formData.lastname" />
  </div>
</template> 

<style scoped>
</style>