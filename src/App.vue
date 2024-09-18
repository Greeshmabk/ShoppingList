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
  data(){
    return{
      tabs: ['Product List', 'Shopping List'], // List of tabs
      activeTab: 'Product List', // Default active tab
    }
  },

   methods: {
    selectTab(tab) {
      this.activeTab = tab;
    },
  },
}
</script>

<template>
   <div class=" shoppingList ">
    <h1 class="text-3xl font-bold text-center underline mx-auto headerPart"><b>Product-Shopping List</b></h1>   
   <!-- Tabs Navigation -->
   <div class="tabs">
      <button
        v-for="(tab, index) in tabs"
        :key="index"
        :class="{ active: activeTab === tab }"
        @click="selectTab(tab)"
      >
        {{ tab }}
      </button>
    </div>
  <div class=" container row justify-center px-8 py-8  ">
   <div class="col-md-6" v-if="activeTab==='Product List'"> <ProductList></ProductList></div>
   <div class="col-md-6" v-if="activeTab==='Shopping List'"> <ShoppingList></ShoppingList></div>
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
  .tabs {
  display: flex;
  margin-bottom: 20px;
  justify-content: center;
}
button {
  padding: 10px 20px;
  cursor: pointer;
  border: none;
  background-color: #eee;
  border-bottom: 2px solid transparent;
  transition: background-color 0.3s;
}

button.active {
  background-color: #ddd;
  border-bottom: 2px solid #42b983;
}

.tab-content {
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}
}
</style>
