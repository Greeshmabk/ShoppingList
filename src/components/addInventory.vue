<script>

export default{
 name: 'Add Product',
 components:{},
 data(){
    return{
        show:  false,
        formattedDate: '',
        expiryDate:''
    }
 },
 methods:{
   async addData(productName,storageLocation,quantity,unit,date){
        
         this.expiryDate = new Date(date).toISOString();
      
        try {
        const response = await fetch('https://shoppinglist.cosmos.cboxlab.com/api/v1/inventory', {
            method: 'POST',
            body: JSON.stringify({
                name: productName,
                quntity:quantity,
                storageLocation:storageLocation,
                unit:unit,
                expiry: this.expiryDate
          })
              
        });
        console.log('Product saved:', response.data);
      } catch (error) {
        console.error('There was an error saving thstorageLocatione product:', error);
      }
        this.show= false;
    }
}
}

</script>
<template>
    <div>
        <div class="button-container py-4">
        <button class="dark:bg-slate-900 dark:text-white "    @click="show=true">Add Product</button>
        </div>
        <div v-if="show" class="modal-overlay" @click.self="close">
            <div class="modal-content">
                <form>
                  <label class="">Product Name:</label>
                  <input type="text" v-model="product">
                  <label class="">Storage Location:</label>
                  <input type="text" v-model="storageLocation">
                  <label class="">Quantity:</label>
                  <input type="number" v-model="quantity">
                  <label class="">Unit:</label>
                  <input type="text" v-model="unit">
                  <label class="">Expiry Date:</label>
                  <input type="date" v-model="date">
                  <button @click="addData(product,storageLocation,quantity,unit,date)">Save</button>  
                </form>
            </div>
        </div>
    </div>
</template>