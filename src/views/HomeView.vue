<template>
    <form >
      <h1 class="display-4 fw-normal">  ADMINSTRATIVE EXAM RESULT SYSTEM </h1>
      <label >Matriculation Number:</label>
      <input type="number" required>
      <label>Examination course:</label>
      <input type="String" required>
      
      <button class="w-100 btn btn-lg btn-primary" type="submit">Check</button>
  </form>
</template>

<script lang="ts">

import { onMounted } from 'vue';
import { useStore } from 'vuex';


export default {
    name: "HomeView",
    setup() {
      
      const store = useStore();
      onMounted(async () => {
        try {
          
       
                await fetch( 'http://localhost:8080/api/user',  {
              
                headers: {'Content-Type': 'application/json'},
                credentials: 'include'
            });

            

            

            await store.dispatch( 'setAuth', true);
          } catch (e) {
            await store.dispatch( 'setAuth', false);

          }
      });

     
     
    }
  }
</script>
