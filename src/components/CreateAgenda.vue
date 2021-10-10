
<template>
  <form @submit.prevent="add">
    <input
      class="form-control"
      type="text"
      placeholder="Title"
      v-model="agenda.title"
    />
    <textarea
      class="form-control"
      placeholder="Description"
      v-model="agenda.description"
    ></textarea>
    <input class="form-control" type="date" v-model="agenda.time" />

    <select class="form-select" v-model="agenda.status">
      <optgroup label="Agenda Status">
        <option value="active" selected="">Active</option>
        <option value="inactive">Inactive</option>
      </optgroup>
    </select>

    <button class="btn btn-primary mt-4" type="submit">Create Agenda</button>
  </form>
</template>

<script>
export default {
  name: "createAgenda",
  data() {
    return {
      agenda: {
        title: "",
        description: "",
        time: "",
        status: "",
      },
    };
  },
  methods: {
    add() {
      this.$emit("app-addAgenda", this.agenda);
      this.agenda = {};
    },
  },
};
</script>
