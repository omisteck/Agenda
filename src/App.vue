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
                        <div class="card-item">
                            <div>
                                <h5 class="agenda-title d-inline-block">Agendas</h5><input type="search" class="d-inline-block" style="margin-left: 10px;" placeholder="Search Agendas">
                            </div>
                            <h6 class="text-text-muted mb-2">Subtitle<span class="status_active">Text</span></h6>
                            <p>Nullam id dolor id nibh ultricies vehicula ut id elit. Cras justo odio, dapibus ac facilisis in, egestas eget quam.&nbsp;<span class="date">On 24th Dec, 2021</span></p><a href="#" data-bs-toggle="modal" data-bs-target="#editModal"><i class="fa fa-edit"></i>&nbsp;Edit</a><a class="m-5 text-danger" href="#"><i class="fa fa-trash-o"></i>&nbsp;Delete</a>
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
                <div class="modal-body">
                    <form><input class="form-control" type="text" placeholder="Title"><textarea class="form-control" placeholder="Description"></textarea><input class="form-control" type="date"><select class="form-select">
                            <optgroup label="Agenda Status">
                                <option value="active" selected="">Active</option>
                                <option value="inactive">Inactive</option>
                            </optgroup>
                        </select></form>
                </div>
                <div class="modal-footer"><button class="btn btn-light" type="button" data-bs-dismiss="modal">Close</button><button class="btn btn-primary" type="button">Update</button></div>
            </div>
        </div>
    </div>
 </div>
</template>

<script>
import CreateAgenda from "./components/CreateAgenda.vue"

export default {
  name: "app",

   components: {
    CreateAgenda
  },
  data: () => ({
    agenda: {
      title: "",
      description: "",
      time: "",
      status: "",
    },
    agendas: [],
    msg : {},
  }),

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
  }
};

</script>

