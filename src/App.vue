<template>
 <div id="app">
    <NavBar/>
  </div>

   <main class="form-signin">
     <router-view/>
</main>
<footer>
  <FooterView/>
</footer>
</template>

<script>
import NavBar from './components/NavBar';
import FooterView from './components/FooterView';

export default {
  name: 'app',
  components: {
    NavBar,
    FooterView,
  }
}
</script>

<style>
html,
body {
  background: #ADD8E6 !important;
      height: 100%;
  
}
.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}

.form-signin .checkbox {
  font-weight: 400;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
