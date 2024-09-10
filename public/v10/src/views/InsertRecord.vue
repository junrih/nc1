<template>
  <div>
    <Navigation/>
  <main class="p-5">
  </main>
  </div>
    <div class="card">
  
      <div class="card-header">
        <h1>Insert Record</h1>
        </div>
      <div class="card-body">
        <table class="table">
          <tbody>
          <tr>
            <td>Last Name</td>
            <td><input v-model="lname" class="form-control" type="text"></td>
          </tr>
          <tr>
            <td>First Name</td>
            <td><input v-model="fname" class="form-control" type="text"></td>
          </tr>
          <tr>
            <td>Age</td>
            <td><input v-model="age" class="form-control" type="number"></td>
          </tr>
          <tr>
            <td></td>
            <td><Button class="btn btn-primary w-100" @click="InsertRecord()">Submit</Button></td>
          </tr>
        </tbody>
        </table>
      </div>

    </div>
    
  
</template>
<script lang="ts">
  import axios from 'axios';
  import Swal from 'sweetalert2'
  import Navigation from '@/components/Navigation.vue';

  export default{
  name: 'InsertRecord',
  components: {Navigation},
  data(){
    return{
      lname: "",
      fname:"",
      age: 0
    }

  },
  methods: {
    async InsertRecord () {
      await axios.get("http://127.0.0.1:8000/api/user/insertRecord/"+this.fname+"/"+this.lname+"/"+this.age).then( async(response) =>{
        Swal.fire({
        title: "Success",
        text: response.data?.message,
        icon: "success"
});
        });
    }
  }
}

</script>
