<template>
  <div >
    <Navigation/>
    <main class="p-5">
      <button class="btn btn-primary" @click="getAllRecord()">Get All Users</button>
      <table class="table table-striped mt-5">
          <tbody>
          <tr v-for="(user, i) in users" :key="i">
            <td>{{ user?.dataid }}</td>
            <td>{{ user?.fname}}</td>
            <td>{{ user?.lname}}</td>
            <td>{{ user?.age}}</td>
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
      await axios.get("http://127.0.0.1:8000/api/user/getAll/").then(async (resposne) =>{
        this.users = resposne.data;
          console.log(resposne.data);
      });

    }
  }

}
</script>

