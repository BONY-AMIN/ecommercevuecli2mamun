<template>
  <div>
    <modal modalHeading="Add New Categry" :cond="showingAddModal" @modalClose="showingAddModal=false">
     <table>
       <tr>
         <td>
           Category Name
         </td>
         <td> <input type="text" id="newCatName" v-model="newCatName.name" placeholder="Category Name"></td>
       </tr>
        <tr>
         <td>
           Category Description
         </td>
         <td><textarea v-model="newCatName.description" type="text" placeholder="Category Description"></textarea> </td>       
       </tr>
       <tr>
         <td></td>
         <td><button class="btnSave" @click="addNewCategory()">Save</button></td>
       </tr>
     </table>
    </modal>
   <h2 class="fleft">Category</h2>
   <button class="addBtn fright" @click="showingAddModal=true">Add New</button>
   <div class="clear"></div>
   <hr>
  </div>
</template>

<script>
export default {
  name: 'Category',
  data () {
    return {
     showingAddModal:false,
     newCatName:{
      name:'',
      description:''
     }
    }
  },
  methods:{
    addNewCategory(){
      this.showingAddModal=false
    }
    
  }
}
</script>
