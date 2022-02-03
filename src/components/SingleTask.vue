<template>
  <div class="task" :class="{ complete: task.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ task.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditTask', params: { id: task.id } }">
          <span class="material-icons"> edit </span>
        </router-link>

        <span @click="deleteTask" class="material-icons"> delete </span>
        <span @click="toggleComplete" class="material-icons tick"> done </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ task.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['task'],

  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/tasks/' + this.task.id,
    };
  },

  methods: {
    deleteTask() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.task.id))
        .catch((err) => console.log(err));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.task.complete }),
      })
        .then(() => {
          this.$emit('complete', this.task.id);
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>
