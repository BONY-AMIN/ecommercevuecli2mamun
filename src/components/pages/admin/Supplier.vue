<template>
  <div>
    <modal modalHeading="Add New Supplier" :cond="showingAddModal" @modalClose="showingAddModal=false">
     <table>
       <tr>
         <td>
           Supplier Name
         </td>
         <td> <input type="text" id="newSupplierName" v-model="newSupplier.name" placeholder="Supplier Name"></td>
       </tr>
        <tr>
         <td>
           Supplier Description
         </td>
         <td><textarea v-model="newSupplier.description" type="text" placeholder="Supplier Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="addNewSupplier()">Save</button></td>
       </tr>
     </table>
    </modal>
    <!-- Edit Modal -->
     <modal modalHeading="Update Supplier" :cond="showingEditModal" @modalClose="showingEditModal=false">
     <table>
       <tr>
         <td>
           Supplier Name
         </td>
         <td> <input type="text" id="newSupplierName" v-model="clickSupplier.name" placeholder="Supplier Name"></td>
       </tr>
        <tr>
         <td>
           Supplier Description
         </td>
         <td><textarea v-model="clickSupplier.description" type="text" placeholder="Supplier Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="updateSupplier(clickSupplier.Id)">Update</button></td>
       </tr>
     </table>
    </modal>
<!-- DELETE -->
    <modal modalHeading="Delete Supplier" :cond="showingDeleteModal" @modalClose="showingDeleteModal=false">
      <h2>You are going to delete the Supplier '{{clickSupplier.name}}'</h2>
     <table>    
       <tr>
         <td><button class="btnSave" @click="DeleteSupplier(clickSupplier.Id)">Yes</button></td>
         <td><button class="btnClose" @click="showingDeleteModal = false">Close</button></td>
       </tr>
     </table>
    </modal>
   <h2 class="fleft">Supplier</h2>
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
     <tr v-for="(it,i) in Supplier">
          <td>{{it.Id}}</td>
          <td>{{it.name}}</td>
          <td>{{it.description}}</td>
          <td><button class="edit" @click="showingEditModal=true;clickSupplier=it;">Edit</button></td>
          <td><button class="delete" @click="showingDeleteModal =true;clickSupplier=it">Delete</button></td>
     </tr>
   </table>
  </div>
</template>

<script>
export default {
  name: 'Supplier',
  data () {
    return {
     showingAddModal:false,
    showingEditModal:false,
    showingDeleteModal:false,
    newSupplier:{
      name:"",
      description:""
    },
    clickSupplier:{},
     Supplier:[]
    }
    },
  methods:{
    addNewSupplier:function(){
           if(!this.newSupplier.name){
           this.$iziToast.error({
        title: 'Error',
        message: 'Illegal operation',
         });
           var newSupplierName=document.getElementById("newSupplierName");
           newCatName.focus();
           return;
     }
      this.Supplier.push({Id:this.Supplier.length + 1,name:this.newSupplier.name,description:this.newSupplier.description});
          this.$iziToast.success({
           title: 'OK',
           message: 'Successfully inserted record!',
              });
      this.showingAddModal=false
    },
    updateSupplier:function(id){
        for(var i = 0; i < this.Supplier.length; i++) {
            if(this.Supplier[i].Id === id) {
               this.Supplier[i].name=this.clickSupplier.name;
                this.Supplier[i].description=this.clickSupplier.description;
                break;
            }
        }
      
       this.showingEditModal = false
    // this.categoris[i].name=this.clickCat.name;
    // this.categoris[i].description=this.clickCat.description;
    
    },
    DeleteSupplier:function(id){
                for(var i = 0; i < this.Supplier.length; i++) {
                    if(this.Supplier[i].Id === id) {
                       this.Supplier.splice(i,1);
                        break;
                    }
                }
                this.showingDeleteModal = false
    }
   
    
  }
}
</script>
