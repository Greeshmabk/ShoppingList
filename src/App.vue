<script >
import ProductList from './components/productList.vue'
import { library } from '@fortawesome/fontawesome-svg-core';
import { faTrash , faEdit } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'; 
import './assets/tailwind.css';
library.add(faTrash , faEdit);


export default{
  name: 'App',
  components:{

    FontAwesomeIcon,
    ProductList   
  },
  
  
}
</script>

<template>
   <div class=" shoppingList ">
    <h1 class="text-3xl font-bold underline mx-auto headerPart"><b>Product-Shopping List</b></h1>   
  
  <div class=" container flex justify-center px-8 py-8  ">
    <ProductList></ProductList>
    <div>
      <div class=" pb-8 flex">
    <h1 class="text-3xl font-bold underline mx-auto headerPart"><b>Shopping List</b></h1>
     
  </div>

  
    </div>
    </div>
</div>
</template>

<style scoped>
.shoppingList{
  background-color: #FFE0BD;
  color: black;
  min-width:1200px;
}
.headerPart {
  line-height: 2.5;
  color: red;
}

.editProduct{
  color: black;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
