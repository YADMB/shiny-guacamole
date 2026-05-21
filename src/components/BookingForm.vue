<template>
  <div class="card">
    <h2 class="title">🎫 Meccsjegy foglalás</h2>

    <div v-if="team" class="selected">
      Kiválasztott csapat: <span>{{ team.name }}</span>
    </div>
    <div v-else class="warning">
      <p>Kérlek, válassz csapatot a táblázatból!</p>
    </div>

    <form @submit.prevent="submitBooking" class="styled-form">
      <div class="input-group">
        <label>Teljes név</label>
        <input v-model="formData.name" type="text" placeholder="Pl.: Teszt Elek" required />
      </div>

      <div class="input-group">
        <label>Email cím</label>
        <input v-model="formData.email" type="email" placeholder="teszt@gmail.com" required />
      </div>

      <button :disabled="isLoading || !team" type="submit" class="submit-btn">
        <span v-if="!isLoading">Jegy igénylése</span>
        <span v-else>⏳ Folyamatban...</span>
      </button>
    </form>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

const props = defineProps({ team: Object });
const isLoading = ref(false);

const formData = reactive({ name: '', email: '' });

const submitBooking = async () => {
  if (!props.team) return;

  isLoading.value = true;
  await new Promise(resolve => setTimeout(resolve, 1500));

  alert(`Sikeres foglalás!\n\nNév: ${formData.name}\nEmail: ${formData.email}\nCsapat: ${props.team.name}`);

  isLoading.value = false;
  formData.name = '';
  formData.email = '';
};
</script>

<style scoped>
.card {
  min-width: 350px;
}

.title {
  text-align: center;
  color: #183686;
  margin-bottom: 1.5rem;
}

.selected {
  background-color: #cfe2fc;
  color: #0030b3;
  padding: 0.75rem;
  border-radius: 8px;
  text-align: center;
  font-weight: 600;
  margin-bottom: 1.5rem;
}

.selected span {
  color: #0043fa;
  text-transform: uppercase;
}

.warning {
  background-color: #fcdada;
  color: #ec2828;
  padding: 0.75rem;
  border-radius: 8px;
  text-align: center;
  font-style: italic;
  margin-bottom: 1.5rem;
}

.styled-form {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-group label {
  font-size: 15px;
  font-weight: 600;
  color: #4b5563;
}

input {
  padding: 0.8rem;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

input:focus {
  outline: none;
  border-color: #3670ce;
}

.submit-btn {
  background: linear-gradient(135deg, #183686 0%, #3670ce 100%);
  color: white;
  padding: 1rem;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  transition: 0.2s;
  margin-top: 1rem;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px #1d5ce64d;
}

.submit-btn:disabled {
  background: #9ca3af;
  cursor: not-allowed;
  opacity: 0.7;
  transform: none;
  box-shadow: none;
}
</style>