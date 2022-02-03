<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="tasks.length">
      <div v-for="task in filteredTasks" :key="task.id">
        <SingleTask :task="task" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleTask from '../components/SingleTask.vue';
import FilterNav from '../components/FilterNav.vue';

export default {
  name: 'Home',
  components: { SingleTask, FilterNav },
  data() {
    return {
      tasks: [],
      current: 'all',
    };
  },

  mounted() {
    fetch('http://localhost:3000/tasks')
      .then((res) => res.json())
      .then((data) => (this.tasks = data))
      .catch((err) => console.log(err.message));
  },

  methods: {
    handleDelete(id) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id;
      });
    },

    handleComplete(id) {
      let p = this.tasks.find((task) => {
        return task.id === id;
      });
      p.complete = !p.complete;
    },
  },

  computed: {
    filteredTasks() {
      if (this.current === 'completed') {
        return this.tasks.filter((task) => task.complete);
      }

      if (this.current === 'ongoing') {
        return this.tasks.filter((task) => !task.complete);
      }

      return this.tasks;
    },
  },
};
</script>
