<template>
 <form @submit.prevent="submit">
     <h1>  ADMINSTRATIVE EXAM RESULT SYSTEM </h1>
    <h1 class="h3 mb-3 fw-normal">Please Register</h1>

    
      <input  v-model="data.name" class="form-control"  placeholder="Name" required>
      <input v-model="data.email" type="email" class="form-control"  placeholder="name@example.com">
      
    
      <input v-model="data.password" type="password" class="form-control" placeholder="Password" required>
      
  
   
    <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
    
      
  </form>
  
</template>

<script lang="ts">
import {reactive} from 'vue'
import { useRouter } from 'vue-router';

export default{
    name: "RegisterView",
    setup(){
        const data = reactive({
            name: '',
            email: '',
            password: ''
        });
        const router = useRouter()

        const submit = async() => {
            await fetch( 'http://localhost:8080/api/registerview',  {
                method: 'POST',
                headers: {'Content-Type': 'application/json;'},
                body: JSON.stringify(data)
            });
            
            await router.push('/loginview');
           

        }

        return {
            data,
            submit
        }
    }
}
</script>
