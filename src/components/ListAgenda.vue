<template>
<div>
<div>
                  <h5 class="agenda-title d-inline-block">Agendas</h5>
                  <input
                    type="search"
                    class="d-inline-block"
                    style="margin-left: 10px"
                    placeholder="Search Agendas"
                    v-model="keyword"
                  />
                </div>
  <div v-for="(agenda, index) of filteredNotes" class="card-item mb-3" :key="agenda.title">
    <h6 class="text-text-muted mb-2">
      {{ agenda.title }}<span :class="{'status_active': agenda.status == 'active', 'btn btn-danger': agenda.status == 'inactive'}" >{{agenda.status}}</span>
    </h6>
    <p>
      {{ agenda.description }}<span class="date"
        >On {{agenda.time}}</span
      >
    </p>
    <a href="#" data-bs-toggle="modal" data-bs-target="#editModal" ><i class="fa fa-edit"></i>&nbsp;Edit</a
    ><a class="m-5 text-danger" href="#" @click="deleteAgenda(index)"
      ><i class="fa fa-trash-o"></i>&nbsp;Delete</a
    >
  </div>
</div>
</template>

<script>
export default {
    props : ['agendas'],

    data() {
        return {
            keyword: "",
        }
    },

    computed: {
    filteredNotes() {
      const { keyword } = this;
      if (!keyword) {
        return this.agendas;
      }
      return this.agendas.filter(({ title, description }) => {
        return title.includes(keyword) || description.includes(keyword);
      });
    },
  },

  methods: {
    deleteAgenda(index) {
      this.$emit("app-deleteAgenda", index);
    },
  }

}
</script>

