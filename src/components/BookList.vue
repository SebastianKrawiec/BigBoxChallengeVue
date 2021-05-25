<template>
<div>
    <div class="state">{{isActive.list_name}}</div>
    <div v-if="books" class="container">
        <ul class="book-list">
                <li class="book-list__item" v-for="book in removeDuplicates()" :key='book.book_uri'>
                <figure class="book-list__item-img">
                    <img class="img" :src='book.book_image' alt="">
                </figure>
                <figcaption class="book-list__item-text">
                    <h5 class="item-text__title">{{book.title}}</h5>
                    <h6 class="item-text__author">{{book.author}}</h6>
                    <p class="item-text__desc">{{book.description}}</p>
                    <a :href='setHref(book)' target="_blank" class="item-text__cta">google it
                    </a>
                </figcaption>
            </li>
        </ul>
    </div>
    <div v-else class="container">
        start searching by selecting a category
    </div>
</div>
    
</template>

<script>
import {API_KEY} from "@/api";
const baseUrl = "https://api.nytimes.com/svc/books/v3";

export default {
  
  name: "BooksLits",
  props:{

      date: String,
      error: [],
      isActive: String
      
  },

  data(){
      return{
          books:[],
      }
  },

  methods:{
       fetchBooks(){

               const booksEndPoint = `/lists/overview.json?published_date=${this.date}&api-key=${API_KEY}`;
               fetch(baseUrl+booksEndPoint)
                .then(res => res.json())
                .then( data => this.books = data.results.lists.map( lista => lista.books).flat())
                .catch( error => this.errors = error);
           
       },
       setHref(data){
           return `https://www.google.com/search?q=${data.author.toLowerCase()}+${data.title.toLowerCase()}`
       },
       removeDuplicates(){
           /* console.log([...new Set(this.books)]) */
            this.books = [...new Set(this.books)];
           return this.books;
           
       }
      
  },

  
  beforeUpdate(){
      this.fetchBooks();

  }
  
  
};

</script>

<style scoped lang="scss">
@import "@/styles/_variables.scss";

.state{
        display: none;
    }

.container{
    position: absolute;
    right: 5vw;
    top: 33vh;
    width: 60vw;
    height: 60vh;
    padding: 2.4rem;
    box-shadow: $--shadow-main;

}

.book-list{

    width: 100%;
    height: 100%;
    overflow-y: scroll;
    display: flex;
    flex-wrap: wrap;
    scrollbar-width: none;
    justify-content: space-between;

    &__item{
        width: calc(95%/2);
        height: 35vh;
        border-right: .5rem solid $--color-main;
        margin-bottom: $--margin-bottom-sm;
        box-shadow: $--shadow-main;
        border-radius: .3rem;
        display: flex;
        justify-content: space-between;

        &-img{
            width: 45%;
            object-fit: fill;
        }

        &-text{
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 1.4rem 2.4rem;
            width: 55%;
            height: 100%;
        }

        
    }

    .item-text__title{
        font-size: 1.6rem;
        font-weight: 600;
        text-transform: capitalize;
    }

    .item-text__author{
        font-size: 1.4rem;
        font-weight: 500;
        text-transform: capitalize;
        margin-bottom: 1rem;
    }

    .item-text__desc{
        font-size: 1.2rem;
        font-weight: 400;
        margin-bottom: 1rem;
        
    }

    .item-text__cta{
        text-align: center;
        width: 100%;
        border: .2rem solid transparent;
        border-radius: .3rem;
        display: inline-block;
        padding: .5rem 1rem;
        text-decoration: none;
        font-size: 1.6rem;
        font-weight: 500;
        color: $--color-main;
        transition: all .2s;
        box-shadow: $--shadow-main;

        &:hover{
            border: .2rem solid $--color-main
        }
    }

    .img{
        width: 100%;
        height: 100%;
    }

    
}



</style>


/* .reduce((acumulador, elemento) => {
                    if(!acumulador.find( aux => aux === elemento)){
                            acumulador.push(elemento)
                    }
                     return acumulador
                }) */