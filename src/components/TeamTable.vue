<template>
  <div class="card table-card">
    <h2 class="title">Csoportkör állása</h2>

    <div class="scroll-container">
      <table>
        <thead>
          <tr>
            <th>Zászló</th>
            <th>Ország</th>
            <th>Pont</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="team in teams" :key="team.id" :class="{ 'active-row': selectedTeamId === team.id }"
            @click="$emit('select-team', team)">
            <td class="flag-cell">
              <div class="selection-indicator"></div>
              <img :src="team.flag" :alt="team.name" class="flag" />
            </td>
            <td class="name">{{ team.name }}</td>
            <td class="pts">{{ team.points }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
defineProps({
  teams: Array,
  selectedTeamId: Number
});

defineEmits(['select-team']);
</script>

<style scoped>
.title {
  text-align: center;
  color: #183686;
  margin-bottom: 1.5rem;
}

.scroll-container {
  max-height: 400px;
  overflow-y: auto;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  position: sticky;
  top: 0px;
  background: #183686;
  color: white;
  z-index: 10;
}

th {
  padding: 12px;
  text-align: left;
  font-size: 15px;
  font-weight: 600;
  cursor: text;
}

tr {
  cursor: pointer;
  position: relative;
  border-bottom: 1px solid #f1f5f9;
}

tr:last-child {
  border-bottom: none;
}

td {
  padding: 12px;
  color: #333;
  font-size: 15px;
}

.flag-cell {
  align-items: center;
  gap: 10px;
}

.selection-indicator {
  position: absolute;
  left: 0px;
  top: 0px;
  bottom: 0px;
  width: 4px;
  background-color: transparent;
}

.active-row {
  background-color: #e4f4ff !important;
}

.active-row .selection-indicator {
  background-color: #4581e0;
}

.flag {
  width: 28px;
  border-radius: 2px;
  box-shadow: 0px 1px 3px #00000030;
}

.name {
  font-weight: 600;
}

.pts {
  font-weight: 800;
  color: #183686;
  text-align: right;
}

.scroll-container::-webkit-scrollbar {
  width: 6px;
}

.scroll-container::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 10px;
}
</style>