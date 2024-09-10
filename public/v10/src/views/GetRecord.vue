<template>
  <div >
    <Navigation/>
    <main class="p-5">
      <button class="btn btn-primary" @click="getAllRecord()">Get All Users</button>
      <table class="table table-striped mt-5">
        <thead>
          <tr>
             <th class="bg-dark text-white">Number</th>
             <th class="bg-dark text-white">First Name</th>
             <th class="bg-dark text-white">Last Name</th>
             <th class="bg-dark text-white">Age</th>
          </tr>
        </thead>
          <tbody>
          <tr v-for="(user, i) in users":key="i">
            <td>{{ user?.dataid }}</td>
            <td>{{ user?.fname}}</td>
            <td>{{ user?.lname}}</td>
            <td>{{ user?.age}}</td>
            <td><button class="btn btn-primary btn-sn" @click="editAge(user)">Edit Age</button></td>
            <td><button class="btn btn-danger btn-sn" @click="deleteRecord(user)">Delete</button></td>
          </tr>
      
        </tbody>
      </table>
    </main>
  </div>
  
</template>
<script lang="ts">
  import axios from 'axios';
  import Swal from 'sweetalert2'
  import Navigation from '@/components/Navigation.vue';
import swal from 'sweetalert';


export default {
  name: "GetRecord",
  components: { Navigation },
  data(){
    return{
    users: {} as any
    }
  },
  methods: {
    async getAllRecord() {
      await axios.get("http://127.0.0.1:8000/api/user/getAll/").then(async (response) =>{
          this.users = response.data;
          console.log(response.data);
      });

    },
    async editAge(user:any) {
      Swal.fire({
        title: "Suwati ug bag-o nga edad",
        input: "text",
        inputAttributes: {
          autocapitalize: "off"
        },
        showCancelButton: true,
      
      }).then(async(result)=>{
        if (result.isConfirmed){
          await axios.get("http://127.0.0.1:8000/api/user/updateRecord/" + user?.dataid + "/" + result.value).then(async()=>{
            this.getAllRecord();
          });
        }
      })
      
    },
    async deleteRecord(user:any) {
      Swal.fire({
        title: "confirmation",
        text: "Delete this user?",
        icon: "warning",
        showCancelButton: true,
        confirmButtonText: "Yes, delete it!",
        cancelButtonText: "No, cancel!",
        reverseButtons: true
      }).then(async(result)=>{
        if (result.isConfirmed){
          await axios.get("http://127.0.0.1:8000/api/user/deleteByID/" + user?.dataid).then(async()=>{
            this.getAllRecord();
          });
        }
      })
      
    }
  }

}
</script>

