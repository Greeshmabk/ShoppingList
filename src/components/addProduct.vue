<script>    
export default {
    name: 'addProduct',
    data() {
    return {
      show:  false,
       
    };
},
methods:{
   async addData(productName){
        console.log(productName)
        try {
        const response = await fetch('https://shoppinglist.cosmos.cboxlab.com/api/v1/shopping-list', {
            method: 'POST',
            body: JSON.stringify({
                name: productName
          })
              
        });
        console.log('Product saved:', response.data);
      } catch (error) {
        console.error('There was an error saving the product:', error);
      }
        this.show= false;
    }
}
}
</script>
<template>
    <div>
        <button @click="show=true">Add Product</button>
        <div v-if="show" class="modal-overlay" @click.self="close">
    <div class="modal-content">
                <form>
                    <label class="">Product Name:</label>
        <input type="text" v-model="product">  
        <button @click="addData(product)">Save</button>       
      </form>
      <button @click="show=false">Close</button>
    </div>
  </div>
    </div>
</template>
<style scoped>
button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
label{
    padding: 20px;
    color: red;
    font-size: 20px;
}
</style>