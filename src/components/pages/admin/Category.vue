<template>
  <div>
    <modal modalHeading="Add New Categry" :cond="showingAddModal" @modalClose="showingAddModal=false">
     <table>
       <tr>
         <td>
           Category Name
         </td>
         <td> <input type="text" id="newCatName" v-model="catname" placeholder="Category Name"></td>
       </tr>
        <tr>
         <td>
           Category Description
         </td>
         <td><textarea v-model="catdes" type="text" placeholder="Category Description"></textarea> </td>       
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
   <table class="nice-table">
     <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Description</th>
            <th>Edit</th>
            <th>Delete</th>             
     </tr>
     <tr v-for="(it,i) in newCatName">
          <td>{{i+1}}</td>
          <td>{{it.name}}</td>
          <td>{{it.description}}</td>
          <td><button class="edit">Edit</button></td>
          <td><button class="delete">Delete</button></td>
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
     catname:'',
     catdes:'',
     newCatName:[]
    }
  },
  methods:{
    addNewCategory(){
      this.newCatName.push({name:this.catname,description:this.catdes});
      this.showingAddModal=false,
      console.log(this.newCatName);
    }
    
  }
}
</script>
