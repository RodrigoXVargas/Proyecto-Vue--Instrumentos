<template>
    <div class="Nav">
      <nav class="Nav-nav">
        <div class="nav-div-content">
          <ul class="nav-div-content-ul">
            <li class="ul-nav__item">
              <router-link to="/">Home</router-link>
            </li>
            <li class="ul-nav__item">
              <router-link to="/crud">Crud</router-link>
            </li>
          </ul>
        </div>
        
      </nav>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'NavBoot'
});
</script>

<style>
.Nav {
    margin: 0;
    padding: 0;
    height: 50px;
    background-image: linear-gradient(to right, #2c3e50 -20%, #42b983 50%, #2c3e50 120%);
    width: 100%;
}

.Nav-nav {
    margin-bottom: 0px;
    padding: 0;
}

.nav-div-content{
    display: grid;
    justify-content: center;
}

.nav-div-content-ul {
    list-style: none;
    margin: 5px;
    padding: 0;
}

.ul-nav__item {
    display: inline-block;
    border-radius: 2px;
    padding: 5px;
}

.ul-nav__item a {
    padding: 2px 5px;
    font-size: 20px;
    color: #000;
    cursor: pointer;
    text-decoration: none;
    border: 2px solid #000;
    border-radius: 10%;
    transition-property: all;
    transition-duration: 0.5s;
}

.ul-nav__item a:hover{
    background-color: #000;
    color: #42b983;
    padding: 5px 20px;
    transition-property: all;
    transition-duration: 0.5s;
}

.ul-nav__item a.router-link-exact-active {
  color: #000;
}

.ul-nav__item a.router-link-exact-active:hover {
  color: #42b983;
}
    
</style>