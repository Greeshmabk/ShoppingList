<script>
import AddInventory from './addInventory.vue'
import '../assets/tailwind.css';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faTrash , faEdit } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'; 
library.add(faTrash , faEdit);

  export default{
    name: 'productList',
    components:{
      AddInventory,
      FontAwesomeIcon
    },
    data(){
      return{
        shoppingList:  this.fetchData(),
        editShow:false, 
        editItem:{}
      };
    },
    methods:{
      fetchData() {    
      fetch('https://shoppinglist.cosmos.cboxlab.com/api/v1/inventory', {
        method: "GET",
        
      })
        .then((response) => {         
          response.json().then((data) => {
            this.shoppingList=data.items;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
    async deleteData(id){
      try {
        const response = await fetch(`https://shoppinglist.cosmos.cboxlab.com/api/v1/inventory/${id}`, {
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
    async editData(editItemDetails){
      try {
        const response = await fetch(`https://shoppinglist.cosmos.cboxlab.com/api/v1/inventory/${editItemDetails.id}`, {
          method: 'POST',
          body: JSON.stringify({
            name: editItemDetails.name,
                quntity:editItemDetails.quntity,
                storageLocation:editItemDetails.storageLocation,
                unit:editItemDetails.unit,
                expiry:editItemDetails.expiry 
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
      this.editItem={};

    }     
    }
  }
</script>

<template>
<div>   
    <div class=" pb-8 flex">
      <h1 class="text-3xl font-bold underline mx-auto headerPart"><b>Product List</b></h1>
    </div>   
    <div>
      <AddInventory></AddInventory> 
      <div class="row">
        <table v-if="!editShow">
          <thead>
            <th>
              <td class="border px-4 py-2 mx-auto">Item Name</td>
              <td class="border px-4 py-2 mx-auto">Expiry date</td>
              <td class="border px-4 py-2 mx-auto">Storage Location</td>
              <td class="border px-4 py-2 mx-auto">Quantity</td>
            </th>
          </thead>
          <tbody>
          <tr v-for="item in shoppingList" :key="index">
            <td class="border px-4 py-2 mx-auto">{{ item.name }}</td>
            <td class="border px-4 py-2 mx-auto">{{ item.expiry }}</td>
            <td class="border px-4 py-2 mx-auto">{{ item.storageLocation }}</td>
            <td class="border px-4 py-2 mx-auto"  >{{ item.quntity+ item.unit}}</td>
            <button @click="editShow=true , editItem=item" class="px-2 py-1 bg-yellow-500 text-white rounded mr-2">
              <font-awesome-icon :icon="['fas', 'edit']" />
            </button>
            <button @click="deleteData(item.id)" class="px-2 py-1 bg-red-600 text-white rounded">
              <font-awesome-icon :icon="['fas', 'trash']" />
            
            </button>
          </tr>
          </tbody> 
        </table>
     <form v-if="editShow"> 
                  <label class="">Product Name:</label>
                  <input type="text" v-model="editItem.name">
                  <label class="">Storage Location:</label>
                  <input type="text" v-model="editItem.storageLocation  ">
                  <label class="">Quantity:</label>
                  <input type="number" v-model="editItem.quntity">
                  <label class="">Unit:</label>
                  <input type="text" v-model="editItem.unit">
                  <label class="">Expiry Date:</label>
                  {{ editItem.expiry }}
                  <input type="date" v-model="editItem.expiry">
                  <button @click="editData(editItem)">Save</button>                 
            </form> 
      </div>
    </div>
</div>
</template>