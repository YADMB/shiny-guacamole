<template>
  <div class="card">
    <h2 class="title">
      <img v-if="team" :src="team.flag" :alt="team.name" class="flag" />
      {{ team ? team.name + ' felállása' : 'Csapat felállása' }}
    </h2>

    <div v-if="team" class="pitch">
      <div class="center-circle"></div>
      <div class="center-circle-dot"></div>
      <div class="row">
        <span v-for="p in team.players.fw" :key="p" class="player fw">{{ p }}</span>
      </div>
      <div class="row">
        <span v-for="p in team.players.mf" :key="p" class="player mf">{{ p }}</span>
      </div>
      <div class="row">
        <span v-for="p in team.players.df" :key="p" class="player df">{{ p }}</span>
      </div>
      <div class="row">
        <span class="player gk">{{ team.players.gk }}</span>
      </div>
    </div>

    <div v-else class="empty-field">
      <p>Válassz csapatot a felállás megtekintéséhez!</p>
    </div>
  </div>
</template>

<script setup>
defineProps({ team: Object });
</script>

<style scoped>
.title {
  text-align: center;
  color: #183686;
  margin-bottom: 1.5rem;
}

.flag {
  width: 32px;
  border-radius: 2px;
  box-shadow: 0px 1px 3px #00000030;
}

.pitch {
  position: relative;
  background-color: #266330;

  background-image:
    linear-gradient(to right, #ffffff59, #ffffff59),
    linear-gradient(to right, #ffffff59, #ffffff59),
    linear-gradient(to right, #ffffff59, #ffffff59),
    linear-gradient(to bottom, transparent 0%, transparent 10%, #ffffff08 10%, #ffffff08 20%, transparent 20%, transparent 30%, #ffffff08 30%, #ffffff08 40%, transparent 40%, transparent 50%, #ffffff08 50%, #ffffff08 60%, transparent 60%, transparent 70%, #ffffff08 70%, #ffffff08 80%, transparent 80%, transparent 90%, #ffffff08 90%, #ffffff08 100%);

  background-position:
    0 25%,
    0 50%,
    0 75%,
    0 0;

  background-size:
    100% 2px,
    100% 2px,
    100% 2px,
    100% 100%;

  background-repeat: no-repeat;
  border-radius: 8px;
  padding: 15px 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 400px;
}

.row {
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: space-evenly;
  gap: 10px;
  width: 100%;
  min-width: 330px;
}

.center-circle {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 120px;
  height: 120px;
  border: 2px solid #ffffff59;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  z-index: 0;
}

.center-circle-dot {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 8px;
  height: 8px;
  background-color: #cececeea;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  z-index: 0;
}

.player {
  background: white;
  color: #183686;
  padding: 6px 10px;
  border-radius: 4px;
  font-size: 0.8rem;
  font-weight: bold;
  min-width: 60px;
  text-align: center;
  box-shadow: 0px 2px 4px #00000030;
}

.gk {
  background: #fcc22f;
  border: 1px solid #aa5b00;
}

.empty-field {
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #9ca3af;
  font-style: italic;
  border: 2px dashed #cbd5e1;
  border-radius: 8px;
  width: 300px;
  text-align: center;
}
</style>