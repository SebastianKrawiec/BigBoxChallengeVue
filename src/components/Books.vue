<template>
  <div class="container">
    <div class="card">
      <div class="heading">
        <div class="img-container">
          <img class="img" src="../../public/img/NYT-logo-150x200px.png" alt="">
        </div>
        <div class="heading__container">
          <h4 class="title">NYTimes Books</h4>
          <h5>{{isActive}}</h5>
        </div>
        
      </div>
      <div class="search">
        <input type="text" class="form-control" placeholder="Search by title" :disabled="!isActive"/>
      </div>
      <div class="content">
        
        <!-- ADD CONTENT HERE -->
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: "Books",
  props:{
    isActive: String
  },
};
</script>

<style scoped lang="scss">
@import "../styles/_variables.scss";

.container {
  z-index: 1;
  position: relative;
  right: -35vw;
  top:5vh;
  max-width: 60vw;
  background-color:$--color-white;
  /* margin: 36px auto; */
  /* max-width: 826px */
}

.card {
  box-shadow: $--shadow-main;
  padding: 24px;
}

.list {
  > li {
    &:not(:last-child) {
      margin-bottom: 18px;
    }
    > a {
      color: #0a5b8c;
      display: block;
      margin-bottom: 6px;
    }

    > span {
      color: rgba(#3b4242, 0.7);
      font-size: 12px;
    }
  }
}

.btn {
  color: #fff;
  cursor: pointer;
  background-color: #117a8b;
  border: 1px solid transparent;
  padding: 6px 12px;
  border-radius: 6px;
  transition: all 0.1s ease-in;
  &:hover {
    background-color: #138496;
    border-color: #117a8b;
  }
}

.heading {
  display: flex;
  align-items: center;
  margin-bottom: 12px;

  .title {
    font-size: 18px;
    font-weight: 600;
    margin-bottom: .3rem;
  }

  .img-container{
    width: 2vw;
    object-fit: fill;
    margin-right: 1rem;
  }

  .img{
    width:100%;
    height: 100%;
  }

  &__container{
   display:flex;
   flex-direction: column;
  }
}
.search {
  margin-bottom: 12px;
  .form-control {
    
    background-color: transparent;
    border: none;
    border-bottom: 1px solid $--color-border;
    outline: 0;
    padding: 6px 0;
    width: 100%;
    /* box-shadow: none; */
    /* border-radius: 0; */
  }
}
</style>
