<template>
  <div class="login">
  <div class="loginHeader">
  	User Login
  </div>
  <div class="loginContainer">
  	<table>
  	<tr>
       <td>User Name</td>
       <td>:</td>
       <td><input type="text" placeholder="User Name" v-model="user.Username"></td>
  	</tr>
  	<tr>
       <td>Password</td>
       <td>:</td>
       <td><input type="Password" placeholder="Password" v-model="user.Password"></td>
  	</tr>
  	<tr>
       <td></td>
       <td></td>
       <td><button class="addBtn" @click="loginNow()">Login</button></td>
  	</tr>
  	</table>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      user:{
        Username:"",
        Password:""
      }
    }
  },
  methods:{
    loginNow(){     
    this.$eventBus.$emit("loadingStatus",true);
     if(this.user.Username == "admin"){
      this.$eventBus.$emit("loadingStatus",false);
      //localStorage:setItem("token",res.data.token);
      this.$router.push({name:"admin"});

     }else{
      this.$eventBus.$emit("loadingStatus",false);
       this.$iziToast.error({
        title: 'Error',
        message: 'Illegal operation',
         });
     }
     
    }
    
  }
}
</script>
