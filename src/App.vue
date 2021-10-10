<template>
 <div>
       <div class="container">
        <div class="row mt-5 mb-4">
            <div class="col text-center">
                <h3>Agenda Application with Vue3</h3>
                <p>Crud system with all function working</p>
            </div>
        </div>
        <div class="row">
            <div class="col card-wrapper">
          <div class="card">
            <div class="card-body">
              
              <div class="alert mb-4" v-if="msg.info"  :class="{'alert-success':msg.type=='success', 'alert-danger':msg.type=='error' }" role="alert">
                {{ msg.info }}</div>
              <h4 class="card-title">Create Agenda</h4>
                <CreateAgenda @app-addAgenda ="add" />
            </div>
          </div>
        </div>
            <div class="col card-wrapper">
          <div class="card">
            <div class="card-body">
              <div >
                
                <ListAgenda :agendas="agendas" @app-deleteAgenda ="deleteAgenda" @app-editAgenda ="editAgenda" />
              </div>
            </div>
          </div>
        </div>
        </div>
    </div>
    <div class="modal fade" role="dialog" tabindex="-1" id="editModal">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">Edit Agenda</h4><button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
              <form @submit.prevent="updaterecord">
    <div class="modal-body">
       
              <div class="alert mb-4" v-if="msg.info"  :class="{'alert-success':msg.type=='success', 'alert-danger':msg.type=='error' }" role="alert">
                {{ msg.info }}</div>
        <input class="form-control" type="text" placeholder="Title" v-model="edit.title" />
        
        <textarea
          class="form-control"
          placeholder="Description"
          v-model="edit.description"
        ></textarea
        >
        <input class="form-control" type="date" v-model="edit.time" />
        <select class="form-select" v-model="edit.status">
          <optgroup label="Agenda Status">
            <option value="active" selected="">Active</option>
            <option value="inactive">Inactive</option>
          </optgroup>
        </select>
    </div>
    <div class="modal-footer">
      <button class="btn btn-light" type="button" data-bs-dismiss="modal">
        Close</button
      ><button class="btn btn-primary" type="submit">Update</button>
      
    </div>
        </form>
            </div>
        </div>
    </div>
 </div>
</template>

<script>
import CreateAgenda from "./components/CreateAgenda.vue"
import ListAgenda from "./components/ListAgenda.vue"

export default {
  name: "app",

   components: {
    CreateAgenda,
    ListAgenda
  },
  data: () => ({
    agenda: {
      title: "",
      description: "",
      time: "",
      status: "",
    },
    edit : {},
    agendas: [],
    msg : {},
  }),
  mounted() {
  if (localStorage.getItem("agendas")){
    this.agendas = JSON.parse(localStorage.getItem("agendas"))
  }
  },

  methods: {
    validate(data){
      if(data.title != '' && data.description != ''  && data.time != ''  && data.status != '' ){
        return true;
      }
      return false;
    },
    add(passAgenda) {
      if(this.validate(passAgenda)){
        this.agendas.push(passAgenda);
        localStorage.setItem('agendas', JSON.stringify(this.agendas))
        this.msg.info = "Agenda saved succesfully!";
        this.msg.type = "success";
      }else{
        this.msg.info = "Please fill all detail to save agenda!";
        this.msg.type = "error";
      }
    },

    editAgenda(record){
      this.indexHandler = record;
      this.edit = this.agendas[record];
    },

    updaterecord(){
        if(this.validate(this.edit)){
          this.agendas[this.indexHandler] = this.edit;
          localStorage.setItem('agendas', JSON.stringify(this.agendas))
          this.msg.info = "Agenda updated succesfully!";
          this.msg.type = "success";

        }

    },  

    deleteAgenda(index){
      this.agendas.splice(index, 1);
      localStorage.setItem('agendas', JSON.stringify(this.agendas))
      this.msg.info = "Agenda deleted successfully!";
      this.msg.type = "success";
    },
  }
};

</script>

