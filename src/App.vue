<template>
  <AppHeader />
  <main class="content">

    <section class="lineup-panel">
      <LineupPanel :team="selectedTeam" />
    </section>

    <section class="team-table">
      <TeamTable :teams="teams" :selectedTeamId="selectedTeam?.id" @select-team="handleSelection" />
    </section>

    <section class="booking-form">
      <BookingForm :team="selectedTeam" />
    </section>

  </main>
  <AppFooter />
</template>

<script setup>
import { ref } from 'vue';
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';
import TeamTable from './components/TeamTable.vue';
import BookingForm from './components/BookingForm.vue';
import LineupPanel from './components/LineupPanel.vue';

import { teamsData } from './data/teams.js';

const teams = ref(teamsData);
const selectedTeam = ref(null);

const handleSelection = (team) => {
  selectedTeam.value = team;
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
  gap: 20px;
  max-width: 1400px;
  margin: 0px auto;
  padding: 2rem 1rem;
  flex: 1;
  width: 100%;
}

.lineup-panel,
.booking-form {
  flex: 0px 0px 350px;
}

.team-table {
  flex: 1;
}

@media (max-width: 1024px) {
  .content {
    flex-direction: column;
    align-items: center;
  }

  .lineup-panel,
  .team-table,
  .booking-form {
    width: 100%;
    max-width: 600px;
    flex: auto;
  }
}
</style>