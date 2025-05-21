<script setup>
import { ref, computed, onMounted, watch } from "vue";
const isLoading = ref(false);
const isUpdate = ref(false);
const isValid = ref(true);
const Firstname = ref("");
const Lastname = ref("");
const Email = ref("");
const error = ref({});

const fullname = computed(() => {
  return `${Firstname.value} ${Lastname.value}`;
});

const updateProfile = async () => {
  isLoading.value = true;
  await new Promise((resolve) => setTimeout(resolve, 2000));
  isLoading.value = false;
  isUpdate.value = true;
  // ตั้งเวลาให้ข้อความ success หายไปหลัง 3 วิ
  setTimeout(() => {
    isUpdate.value = false;
  }, 3000); // 3000ms = 3 seconds
};

const validatedName = (name) => {
  const re = /\d/;
  return !re.test(name);
};

const validatedEmail = (email) => {
  return email.includes("@");
};

watch([Firstname, Lastname, Email], () => {
  isValid.value = true;
  isUpdate.value = false;
  error.value = {};

  if (!validatedName(Firstname.value)) {
    isValid.value = false;
    error.value.Firstname = "Firstname must not contain numbers";
  }

  if (!validatedName(Lastname.value)) {
    isValid.value = false;
    error.value.Lastname = "Lastname must not contain numbers";
  }

  if (!validatedEmail(Email.value)) {
    isValid.value = false;
    error.value.Email = "Email must contain @";
  }
});

onMounted(() => {
  Firstname.value = "test";
  Lastname.value = "test";
  Email.value = "test@email.com";
});
</script>

<template>
  <div class="container">
    <div>
      <div class="form-row">Fullname : {{ fullname }}</div>
      <div class="form-row">email : {{ Email }}</div>
    </div>
    <div class="form-row">
      <label>Firstname:</label>
      <input type="text" v-model="Firstname" />
      <div>{{ error.Firstname }}</div>
    </div>
    <div class="form-row">
      <label>Lastname:</label>
      <input type="text" v-model="Lastname" />
      <div>{{ error.Lastname }}</div>
    </div>
    <div class="form-row">
      <label>Email:</label>
      <input type="text" v-model="Email" />
      <div>{{ error.Email }}</div>
    </div>
    <div v-if="isLoading" class="loading">loading...</div>
    <button :disabled="!isValid" class="button" @click="updateProfile()">
      Update Profile
    </button>
    <div v-if="isUpdate" class="alert-success">
      Profile updated successfully.
    </div>
  </div>
</template>

<style>
.alert-success {
  background: linear-gradient(135deg, #1dd1a1, #10ac84);
  color: white;
  padding: 15px 20px;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  font-weight: bold;
  text-align: center;
  transition: all 0.3s ease;
  margin-top: 20px;
  animation: fadeIn 0.5s ease-in-out;
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 320px;
  margin: 0 auto;
}

.container > div {
  width: 100%;
}

.loading {
  background-colour: aliceblue;
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
}
.button {
  width: 100%;
  height: 50px;
  margin-top: 20px;
}
input {
  width: 100%;
}

.form-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  margin-top: 10px;
}

.form-row label {
  width: 80px;
  text-align: right;
}

.form-row input {
  flex: 1;
}

.error-message {
  color: #ff6b6b;
  font-size: 0.75rem; /* เล็กลงจากเดิม */
  margin-top: 4px;
  margin-left: 4px;
  line-height: 1.2;
  font-weight: 400;
}
</style>
