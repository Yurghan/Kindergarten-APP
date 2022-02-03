<template>
  <form @submit.prevent="handleSubmit">
    <label>Nazwa zadania</label>
    <input type="text" v-model="title" required />
    <label>Opis zadania</label>
    <textarea v-model="details" required></textarea>
    <button>Dodaj zadanie</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      details: '',
    };
  },
  methods: {
    handleSubmit() {
      let task = {
        title: this.title,
        details: this.details,
        complete: false,
      };

      fetch('http://localhost:3000/tasks', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(task),
      })
        .then(() => {
          this.$router.push('/');
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>
