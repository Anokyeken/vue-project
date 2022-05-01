<template>
    <form @submit.prevent="submit">
      <h1 class="display-4 fw-normal">  ADMINSTRATIVE EXAM RESULT SYSTEM </h1>
    <h2 class="h3 mb-3 fw-normal">Please sign in</h2>

    
      <input v-model="data.email" type="email" class="form-control"  placeholder="name@example.com">
      
    
      <input v-model="data.password" type="password" class="form-control" placeholder="Password">
      
  
   
    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    
  </form>
</template>

<script lang="ts">
import { reactive } from '@vue/reactivity';
import { useRouter } from 'vue-router';

export default{
    name: "LoginView",
    setup() {
       const data = reactive( {
      email: '',
      password: ''
    });

    const router = useRouter();

    const submit = async() => {
       await fetch( 'http://localhost:8080/api/loginview',  {
                method: 'POST',
                headers: {'Content-Type': 'application/json;'},
                credentials: 'include',
                body: JSON.stringify(data)
            });

            await router.push('/');

    }

    return {
      data,
      submit
     }
   
    }
}

</script>
