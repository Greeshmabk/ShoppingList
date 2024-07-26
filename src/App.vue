<script >
import AddProduct from './components/addProduct.vue'
import { library } from '@fortawesome/fontawesome-svg-core';
import { faTrash , faEdit } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'; 
import './assets/tailwind.css';
library.add(faTrash , faEdit);


export default{
  name: 'App',
  components:{
    AddProduct,
    FontAwesomeIcon,       
  },
  data() {
    return {
      shoppingList:  this.fetchData(),
      editShow:false, 
      editItem:''
    };
  },
    methods: {
    fetchData() {
      fetch('https://shoppinglist.cosmos.cboxlab.com/api/v1/shopping-list', {
        method: "GET",
        
      })
        .then((response) => {
          response.json().then((data) => {
           
            this.shoppingList=data;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
   async deleteData(id){
      try {
        const response = await fetch(`https://shoppinglist.cosmos.cboxlab.com/api/v1/shopping-list/${id}`, {
          method: 'DELETE'
        });
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        console.log(`Product with ID ${id} deleted.`);
      this.fetchData()
      } catch (error) {
        console.error('There was an error deleting the product:', error);
      }

    },
    async editData(id,productName){
      try {
        const response = await fetch(`https://shoppinglist.cosmos.cboxlab.com/api/v1/shopping-list/${id}`, {
          method: 'POST',
          body: JSON.stringify({
                name: productName
          })
        });
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        console.log(`Product with ID ${id} edited       .`);
      this.   fetchData()
      } catch (error) {
        console.error('There was an error editing the product:', error);
      }

    }
  },
  
}
</script>

<template>
  <div>
  <div class=" pb-8 flex">
    <h1 class="text-3xl font-bold underline headerPart"><b>Shopping List</b></h1>
    <AddProduct></AddProduct>  
  </div>

  <div>
  <div class="row">
    <ul>
      <li class="pb-2 " v-for="item in shoppingList.items" :key="index">
        {{ item.name }}
        <button class="pl-8 pr-8" @click="editShow=true , editItem=item.id"><FontAwesomeIcon :icon="['fas', 'edit']" /></button>  
        <button class="" @click="deleteData(item.id)"><FontAwesomeIcon :icon="['fas', 'trash']" class="mr-2" /></button>
        
      </li>
    </ul>
    <form v-if="editShow"> 
                    <label class="">Product Name:</label>
        <input class="editProduct" type="text" v-model="product">  
        <button @click="editData(editItem,product)">Save</button>       
      </form>
      
  </div>  
</div>
  </div>
</template>

<style scoped>

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
