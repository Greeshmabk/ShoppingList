<script >
import AddProduct from './components/addProduct.vue'
import { library } from '@fortawesome/fontawesome-svg-core';
import { faTrash } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'; 

library.add(faTrash);


export default{
  name: 'App',
  components:{
    AddProduct,
    FontAwesomeIcon       
  },
  data() {
    return {
      shoppingList:  this.fetchData(),
      editShow:false
       
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
      this.   fetchData()
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
        console.error('There was an error deleting the product:', error);
      }

    }
  },
  
}
</script>

<template>
  <header>
    <h1><b>Shopping List</b></h1>
  </header>

  <main>
  <div class="row">
    <ul>
      <li v-for="item in shoppingList.items" :key="index">
        {{ item.name }}
           
        <button @click="deleteData(item.id)"><FontAwesomeIcon :icon="['fas', 'trash']" class="mr-2" /></button>
        <button @click="editShow=true">Edit Data</button>
        <form v-if="editShow"> 
                    <label class="">Product Name:</label>
        <input type="text" v-model="product">  
        <button @click="editData(item.id,product)">Save</button>       
      </form>
      </li>
    </ul>
  </div>
   <AddProduct></AddProduct>    
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
