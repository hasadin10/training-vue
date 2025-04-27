<script setup>
import { reactive } from "vue";
const genderList = ["man", "women", "other"];
const interestList = ["sports", "music", "art"];
const formData = reactive({ interests: [] });
const submitForm = () => {
  console.log("Form submitted");
  console.log("formData", formData);
  console.log("interests", formData.interests);
};
</script>

<template>
  <div>
    <div>
      <div>Firstname</div>
      <input type="text" name="firstname" v-model="formData.firstname" />
    </div>
    <div>
      <div>Lastname</div>
      <input type="text" name="lastname" v-model="formData.lastname" />
    </div>

    <div>
      <div>Gender</div>
      <div v-for="gender in genderList">
        <input
          type="radio"
          name="gender"
          :value="gender"
          v-model="formData.gender"
        />
        {{ gender }}
      </div>
    </div>
    <div>
      <div>Interests</div>
      <div v-for="interest in interestList">
        <input
          type="checkbox"
          name="interest"
          :value="interest"
          v-model="formData.interests"
        />
        {{ interest }}
      </div>
    </div>
    <div>
      <div>Description</div>
      <textarea v-model="formData.description"></textarea>
    </div>
    <button @click="submitForm">Submit</button>
  </div>
</template>

<style></style>
