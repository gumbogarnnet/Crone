<template>

    <div>
      
      <mdb-tbl class="table table-responsive table-hover table-borderless table-striped">
        <mdb-tbl-head color="grey">
          <tr>
            <th scope="col">Task id</th>
            <th scope="col" >Task Name</th>
            <th scope="col">Task Time</th>
            <th scope="col">Task Type</th>
            <th scope="col">Action</th>
          </tr>
        </mdb-tbl-head>
        <mdb-tbl-body>
          
          <tr :style="{ cursor: 'pointer'}" v-for="(garnnet, index) in info" :key="index">
            
            <td >{{garnnet.tId}}</td>
            <td >{{garnnet.taskDesc}}</td>
            <td >{{garnnet.taskTime}}</td>
            <td>{{garnnet.taskType}}</td>
            <td> <mdb-btn v-on:click="deleteById(garnnet.tId, index)" color="danger" ><i class="fa fa-trash "></i></mdb-btn><mdb-btn color="primary" v-on:click="getAllTasKById(garnnet.tId)"><i class="fa fa-eye "></i></mdb-btn> </td>
          </tr>
          
          
  
        </mdb-tbl-body>
      </mdb-tbl>
      

       
      <mdb-modal :show="modal" @close="modal = false">
      <mdb-modal-header>
      <mdb-modal-title><label>Task Number: {{infoById.tId}}</label></mdb-modal-title>
      </mdb-modal-header>
      <mdb-modal-body>
       
       
            
       
        <br/>
       <label>Task Description</label>
        <input :value="infoById.taskDesc" class="form-control form-control-sm" type="text" > <br/>
        <label>Task Type</label>
        <input :value="infoById.taskType" class="form-control form-control-sm" type="text" ><br/>
        <label>Task Time</label>
        <input :value="infoById.taskTime" class="form-control form-control-sm" type="text" ><br/>
        <label>Command</label>
        <input :value="infoById.cmd" class="form-control form-control-sm" type="text" ><br/>
        <label>Status</label>
        <input :value="infoById.active" class="form-control form-control-sm" type="text"><br/>
        
        

      </mdb-modal-body>
      <mdb-modal-footer>
      
      <mdb-btn color="primary">Save changes</mdb-btn>
      </mdb-modal-footer>
    </mdb-modal>

      
    </div>
  </template>


<script>
  import { mdbTbl, mdbTblHead, mdbTblBody, mdbModal, mdbModalHeader, mdbModalTitle, mdbModalBody, mdbModalFooter, mdbBtn } from 'mdbvue';

  export default {
    name: 'TablePage',
     data () {
    return {
      info: [],
      infoById:[],
      modal: false
    }
  },
    components: {
      mdbTbl,
      mdbTblHead,
      mdbTblBody,
      mdbModal,
      mdbModalHeader,
      mdbModalTitle,
      mdbModalBody,
      mdbModalFooter,
      mdbBtn,
    },
    clickList: function (product) {
    console.log("clickList fired with " + product.id);
    },
    methods: {
      getAllTasks(){
        axios
              .get('http://localhost:8080/taskall')
              .then(response => (this.info = response.data))
      },
      getAllTasKById(id,){
        
        this.modal = true;
        axios
        .get('http://localhost:8080//taskbyid?tId=' +id)
        .then(response => (this.infoById = response.data))

      },
    
    deleteById(id, index){
        console.log(index)
              
        axios
        .delete('http://localhost:8080/delbyid?tId=' +id)
        
         this.info.splice(index, 1)
         
      },
            
      
    },
    

     mounted () {
       this.getAllTasks();
        
  }
}
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
