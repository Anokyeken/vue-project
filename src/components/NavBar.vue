
<template>


    <nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
    <div class="container-fluid">
        <router-link to="/" class="navbar-brand">Home</router-link>
    
        <div >
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="!auth">
            <li class="nav-item">
            <router-link to="/loginview" class="nav-link active">Login</router-link>
            </li>
            <li class="nav-item">
            <router-link to="/registerview" class="nav-link active">Register</router-link>
            </li>
        </ul>
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="auth">
            <li class="nav-item">
            <router-link to="/loginview" class="nav-link active" @click="logout">Logout</router-link>
            </li>
            
        </ul>
        
        </div>
    </div>
    </nav>
  
</template>
<script lang="ts">
import { useStore } from 'vuex';
import { computed } from 'vue';

export default {
  name: 'NavBar',
  setup() {
      const store = useStore();
      const auth = computed( () => store.state.authenticated)  

      const logout = async () => {
          await fetch( 'http://localhost:8081/api/logout',  {
                method: 'POST',
                headers: {'Content-Type': 'application/json;'},
                credentials: 'include',
               
            });

      }
      return {
          auth
      }
  }
};
 
</script>
