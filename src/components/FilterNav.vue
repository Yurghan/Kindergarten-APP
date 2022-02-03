<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">Pokaż wszystkie</button>
    <button @click="updateFilter('completed')" :class="{ active: current === 'completed' }">Wykonane</button>
    <button @click="updateFilter('ongoing')" :class="{ active: current === 'ongoing' }">Do zrobienia</button>
  </nav>
</template>

<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(by) {
      this.$emit('filterChange', by);
    },
  },
};
</script>
