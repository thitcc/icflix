<template>
  <div id="app">
    <div id="nav1">
        <ul id="nav2">
          <li class="title"><a href="/">ICFlix</a></li>
          <li class="op-li" v-if="this.$route.name == 'home'"><a href="#" @click="navegar()" id="link">Categorias</a></li>
          <li class="op-li admin"><a :href="process.env.VUE_APP_API + 'admin'">Admin</a></li>
        </ul>
    </div>
    <menu-categoria v-if="showMenuCategories"/>
    <router-view id="container-top"/>
  </div>
</template>

<script>
import MenuCategoria from './components/MenuCategoria.vue'
import EventBus from './eventBus'
export default {
  data: () => ({
    showMenuCategories: false
  }),
  components: {
    "menu-categoria": MenuCategoria
  },
  methods: {
    navegar() {
      if (this.showMenuCategories) {
        EventBus.$emit('returnHome')
      }
      this.showMenuCategories = !this.showMenuCategories
    },
  }
}
</script>

<style>

#nav2 .admin{
  float: right;
  cursor: pointer;
}

#container-top {
  margin-top: 100px;
}

html {
  scroll-behavior: smooth;
}

html,body {
  min-height: 100%;
  height: 100%;
  width: 100%;
}

ul {
  margin: 0;
  height: 100px;
}

body {
    background-color: #444444;
    font-family: 'Comfortaa', cursive;
    margin: 0 !important;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

#nav1 {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 4;
    background-color: rgba(68, 68, 68, 0.7);
}

#nav2 {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    transition: all 0.6s ease-out;
}

ul li {
    float: left;
}

li a {
    color: whitesmoke;
    text-decoration: none;
    transition: all 0.5 ease;
}

li a :hover {
    font-size: 18px;
}

.op-li {
    display: inline-block;
    margin: 0 10px 0 0;
    padding: 15px 45px;
    font-size: 16px;
    line-height: 4;
    box-shadow: none;
    border-radius: 0;
}

.title {
    display: inline-block;
    margin: 0 10px 0 0;
    padding: 15px 45px;
    font-size: 30px;
    line-height: 1.8;
    box-shadow: none;
    border-radius: 0;
    font-family: 'Righteous', cursive;
    color: whitesmoke;
}

</style>
