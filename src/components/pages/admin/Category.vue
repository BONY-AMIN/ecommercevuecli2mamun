<template>
  <div>
    <modal modalHeading="Add New Category" :cond="showingAddModal" @modalClose="showingAddModal=false">
     <table>
       <tr>
         <td>
           Category Name
         </td>
         <td> <input type="text" id="newCatName" v-model="newCat.name" placeholder="Category Name"></td>
       </tr>
        <tr>
         <td>
           Category Description
         </td>
         <td><textarea v-model="newCat.description" type="text" placeholder="Category Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="addNewCategory()">Save</button></td>
       </tr>
     </table>
    </modal>
    <!-- Edit Modal -->
     <modal modalHeading="Update Category" :cond="showingEditModal" @modalClose="showingEditModal=false">
     <table>
       <tr>
         <td>
           Category Name
         </td>
         <td> <input type="text" id="newCatName" v-model="clickCat.name" placeholder="Category Name"></td>
       </tr>
        <tr>
         <td>
           Category Description
         </td>
         <td><textarea v-model="clickCat.description" type="text" placeholder="Category Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="updateCategory(clickCat.Id)">Update</button></td>
       </tr>
     </table>
    </modal>
<!-- DELETE -->
    <modal modalHeading="Delete Category" :cond="showingDeleteModal" @modalClose="showingDeleteModal=false">
      <h2>You are going to delete the category '{{clickCat.name}}'</h2>
     <table>    
       <tr>
         <td><button class="btnSave" @click="DeleteCat(clickCat.Id)">Yes</button></td>
         <td><button class="btnClose" @click="showingDeleteModal = false">Close</button></td>
       </tr>
     </table>
    </modal>
   <h2 class="fleft">Category</h2>
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
     <tr v-for="(it,i) in categoris">
          <td>{{it.Id}}</td>
          <td>{{it.name}}</td>
          <td>{{it.description}}</td>
          <td><button class="edit" @click="showingEditModal=true;clickCat=it;">Edit</button></td>
          <td><button class="delete" @click="showingDeleteModal =true;clickCat=it">Delete</button></td>
     </tr>
   </table>
  </div>
</template>

<script>
export default {
  name: 'Category',
  data () {
    return {
     showingAddModal:false,
    showingEditModal:false,
    showingDeleteModal:false,
    newCat:{
      name:"",
      description:""
    },
    clickCat:{},
     categoris:[]
    }
    },
  methods:{
    addNewCategory:function(){
           if(!this.newCat.name){
           this.$iziToast.error({
        title: 'Error',
        message: 'Illegal operation',
         });
           var newCatName=document.getElementById("newCatName");
           newCatName.focus();
           return;
     }
      this.categoris.push({Id:this.categoris.length + 1,name:this.newCat.name,description:this.newCat.description});
          this.$iziToast.success({
           title: 'OK',
           message: 'Successfully inserted record!',
              });
      this.showingAddModal=false
    },
    updateCategory:function(id){
        for(var i = 0; i < this.categoris.length; i++) {
            if(this.categoris[i].Id === id) {
               this.categoris[i].name=this.clickCat.name;
                this.categoris[i].description=this.clickCat.description;
                break;
            }
        }
      
       this.showingEditModal = false
    // this.categoris[i].name=this.clickCat.name;
    // this.categoris[i].description=this.clickCat.description;
    
    },
    DeleteCat:function(id){
                for(var i = 0; i < this.categoris.length; i++) {
                    if(this.categoris[i].Id === id) {
                       this.categoris.splice(i,1);
                        break;
                    }
                }
                this.showingDeleteModal = false
    }
   
    
  }
}
</script>
