<template>
  <h1>Organizer Nauczyciela Przedszkolnego</h1>
  <Navbar />
  <router-view />
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: { Navbar },
};
</script>
