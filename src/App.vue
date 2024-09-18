<script >
import ProductList from './components/productList.vue'
import './assets/tailwind.css';
import ShoppingList from './components/shoppingList.vue';


export default{
  name: 'App',
  components:{
    ProductList,
    ShoppingList   
  },
  
  
}
</script>

<template>
   <div class=" shoppingList ">
    <h1 class="text-3xl font-bold text-center underline mx-auto headerPart"><b>Product-Shopping List</b></h1>   
  
  <div class=" container flex justify-center px-8 py-8  ">
    <ProductList></ProductList>
    <ShoppingList></ShoppingList>
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
