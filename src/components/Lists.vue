<template>
    <div class="container">
        <h2 class="title title--list">your booklist:</h2>

        <ul class="list">
            <li class="list__item" v-for="item in filteredLists()" 
            @click="isActive(item)"
            :key="item.list_name_encoded">
                {{item.list_name}}
            </li>
        </ul>
    </div>
</template>

<script>
import {API_KEY} from "@/api";
const baseUrl = "https://api.nytimes.com/svc/books/v3";
const listEndPoint = `/lists/names.json?api-key=${API_KEY}`;


export default {
  name: "LitsName",
  data(){
      return{ 
        lists: [],
        errors : "",
        active:{}
    }
  },
  methods:{
      filteredLists(){
          let filteredData = this.lists.filter( ele => this.lists.indexOf(ele) < 10);
          return filteredData
      },
      isActive(item){  
          this.$emit("active", item);
      }
      
  },
  mounted(){
      
      fetch(baseUrl+listEndPoint)
        .then(res => res.json())
        .then( data => this.lists = data.results)
        .catch( error => this.errors = error);
  }

}


</script>

<style scoped lang="scss">

@import "@/styles/_variables.scss";

    .container{
        
        height: 88vh;
        position: absolute;
        left: 5vw;
        top: 5vh;
        background-color:$--color-white;
        padding: 2.4rem;
        box-shadow: $--shadow-main;
        width:20vw;
        display: flex;
        flex-direction: column;
        justify-content: space-around;

        .list{
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            overflow-y: scroll;
            scrollbar-width: none;
            
            &__item{
                display: inline-block;
                text-align: center;
                font-size: 1.2rem;
                font-weight: 500;
                color: $--color-letter;
                width: 100%;
                padding: 1.5rem 1rem;
                cursor: pointer;
                box-shadow: $--shadow-main;
                border: .1rem solid $--color-border;
                border-bottom: .2rem solid $--color-main;
                transition: all .2s;
                


                &:not(:last-child){
                    margin-bottom: $--margin-bottom-sm;
                }

                &:hover{
                    color: $--color-white;
                    background-color: $--color-main;
                    border: .1rem solid $--color-main;
                    border-bottom: .2rem solid $--color-border;
                }

                &:active{
                    background-color: $--color-main;
                    opacity: .6;
                }
            }

        }

        .title--list{
            margin-bottom: $--margin-bottom-sm;
        }
    }


    

</style>