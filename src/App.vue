<template>
  <div id="app">
    <div class="navbar">
      <ListsName @active="setActive"/>
      <Books :isActive="active.list_name" />
      <BooksLits :date="active.newest_published_date" :isActive="active.list_name" />
      
      <!-- pasarle al componente la prop 
      :nombreProp="datos"
      :isActive="active"
      -->
    </div>
  </div>
</template>

<script>
import Books from "./components/Books.vue";
import ListsName from "./components/Lists.vue";
import BooksLits from "./components/BookList.vue";

export default {
  name: "app",
  components: {
    Books,
    ListsName,
    BooksLits
  },
  data(){
    return{
      active: {},
    }
  }
  ,
  methods:{
    setActive(nombreLista){
     return this.active = nombreLista
    },

    
  }
};
</script>

<style lang="scss">
@import "./styles/_variables.scss";
@import "./styles/main.scss";

.navbar {
  /* background-color: $--color-main; */
  background-image: linear-gradient(200deg, $--color-main, $--color-secondary);
  width: 100%;
  height: 96px;
  position: absolute;
  z-index: 0;
}

</style>
