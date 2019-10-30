<template>
  <!-- Material form register -->
  <div class="col-6 center">
  <form class="login"  @submit="createtask()" action="/Home">

      <div class="row d-flex justify-content-center mt-2">
    <i class="fas fa-book fa-10x"></i>
    </div>
      
    <p class="h4 text-center mb-4">Add your Task here</p>
    <div class="grey-text">
      <mdb-input label="Task Description" icon="user" type="text" v-model="taskDesc"/>
      <mdb-input label="Task Time" icon="envelope" type="text" />
      <mdb-input label="Task type" icon="exclamation-triangle" type="text" v-model="taskType"/>
    </div>
    <div class="text-center">
      <mdb-btn color="primary" >Add</mdb-btn>
    </div>
  </form>
  {{message}}
  </div>
  <!-- Material form register -->
</template>
<script>
  import { mdbInput, mdbBtn } from 'mdbvue';
  export default {
    name: 'Basic',
    data(){
      return{
      taskTime: "* * * * * *" ,
      taskDesc:"",
      taskType:"",
      cmd:"",
      active: false,
      
      }
       
    },
     props: ['message'],
    components: {
      mdbInput,
      mdbBtn
    },
    methods:{

    createtask(){
    axios.post('http://localhost:8080/createTask', {
    
    
    taskDesc:this.taskDesc,
    taskType:this.taskType,
    cmd:this.cmd,
    active: true,
    taskTime: this.taskTime ,
  })
    then(response => {
      self.message = 'Data is entered'
  })
  .catch(function (error) {
    console.log(error);
  })

     }
    },

    mounted() {
            console.log('Component mounted.')
        },
    
  }

</script>

<style scoped>
.center {
  margin: auto;
}
</style>