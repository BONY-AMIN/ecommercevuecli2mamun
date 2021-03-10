<template>
  <div>
    <modal modalHeading="Add New Product" :cond="showingAddModal" @modalClose="showingAddModal=false">
     <table>
       <tr>
         <td>
           Product Name
         </td>
         <td> <input type="text" id="newProductName" v-model="newProduct.name" placeholder="Product Name"></td>
       </tr>
       <tr>
        <td>
        Category 
       </td><td>
         <select v-model="newProduct.category">
           <option value="">---Select---</option>
           <option v-for="c in categoris" value="c.Id">
             {{c.name}}
           </option>
         </select>
       </td>
     </tr>
      <tr>
        <td>
        Supplier 
       </td><td>
         <select v-model="newProduct.supplier">
           <option value="">---Select---</option>
           <option v-for="s in suppliers" value="s.Id">
             {{s.name}}
           </option>
         </select>
       </td>
     </tr>
      <tr>
         <td>
           Price
         </td>
         <td> <input type="text" v-model="newProduct.price" placeholder="Price">
          <label><input type="checkbox" v-model="newProduct.negotiable">Negotiable</label></td>
       </tr>
       <tr>
         <td>
           Image
         </td>
         <td> <input type="file" id="image" @change="onFileChange">
          </td>
       </tr>
       <tr>
         <td>       
         </td>
         <td> 
          <progress :value="parcent" max="100" v-if="parcent != 0 && parcent != 100"></progress>
          <span v-if="parcent != 0 && parcent != 100"></span>
          <img :src="newProduct.image" alt="No Image Selected" class="thumbnile">
          </td>
       </tr>
        <tr>
         <td>
           Product Description
         </td>
         <td><textarea v-model="newProduct.description" type="text" placeholder="Product Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="addNewProduct()">Save</button></td>
       </tr>
     </table>
    </modal>
    <!-- Edit Modal -->
     <modal modalHeading="Update Product" :cond="showingEditModal" @modalClose="showingEditModal=false">
     <table>
       <tr>
         <td>
           Product Name
         </td>
         <td> <input type="text" id="newProductName" v-model="clickProduct.name" placeholder="Product Name"></td>
       </tr>
        <tr>
         <td>
           Product Description   
         </td>
         <td><textarea v-model="clickProduct.description" type="text" placeholder="Product Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="updateProduct(clickProduct.Id)">Update</button></td>
       </tr>
     </table>
    </modal>
<!-- DELETE -->
    <modal modalHeading="Delete Product" :cond="showingDeleteModal" @modalClose="showingDeleteModal=false">
      <h2>You are going to delete the Product '{{clickProduct.name}}'</h2>
     <table>    
       <tr>
         <td><button class="btnSave" @click="DeleteProduct(clickProduct.Id)">Yes</button></td>
         <td><button class="btnClose" @click="showingDeleteModal = false">Close</button></td>
       </tr>
     </table>
    </modal>
   <h2 class="fleft">Product</h2>
   <button class="addBtn fright" @click="showingAddModal=true">Add New</button>
   <div class="clear"></div>
   <hr>
   <table class="nice-table">
     <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Description</th>
            <th>Edit</th>
            <th>Delete</th>             
     </tr>
     <tr v-for="(it,i) in Product">
          <td>{{it.Id}}</td>
          <td>{{it.name}}</td>
          <td>{{it.description}}</td>
          <td><button class="edit" @click="showingEditModal=true;clickProduct=it;">Edit</button></td>
          <td><button class="delete" @click="showingDeleteModal =true;clickProduct=it">Delete</button></td>
     </tr>
   </table>
  </div>
</template>

<script>
export default {
  name: 'Product',
  data () {
    return {
     showingAddModal:false,
    showingEditModal:false,
    showingDeleteModal:false,
    categoris:
    [{name:'Mobile',Id:1},
    {name:'Honda',Id:2},
    {name:'Sports',Id:3}],

     suppliers:
    [{name:'Bony',Id:1},
    {name:'Rafee',Id:2},
    {name:'Anik',Id:3}],
    newProduct:{
      name:"",
      description:"",
      supplier:"",
      category:"",
      prce:0,
      negotiable:true,
      image:"img/uploads/default.jpg"
    },
    parcent:0,
    clickProduct:{},
     Product:[]
    }
    },
  methods:{
    addNewProduct:function(){
           if(!this.newProduct.name){
           this.$iziToast.error({
        title: 'Error',
        message: 'Illegal operation',
         });
           var newProductName=document.getElementById("newProductName");
           newCatName.focus();
           return;
     }
      this.Product.push({Id:this.Product.length + 1,name:this.newProduct.name,description:this.newProduct.description});
          this.$iziToast.success({
           title: 'OK',
           message: 'Successfully inserted record!',
              });
      this.showingAddModal=false
    },
    updateProduct:function(id){
        for(var i = 0; i < this.Product.length; i++) {
            if(this.Product[i].Id === id) {
               this.Product[i].name=this.clickProduct.name;
                this.Product[i].description=this.clickProduct.description;
                break;
            }
        }
      
       this.showingEditModal = false
    // this.categoris[i].name=this.clickCat.name;
    // this.categoris[i].description=this.clickCat.description;
    
    },
    DeleteProduct:function(id){
                for(var i = 0; i < this.Product.length; i++) {
                    if(this.Product[i].Id === id) {
                       this.Product.splice(i,1);
                        break;
                    }
                }
                this.showingDeleteModal = false
    }
   
    
  }
}
</script>
