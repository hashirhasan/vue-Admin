<template>
<div>
  <div class="row"  v-if="editseen" >
     <div class="col-2">{{user.name}}</div>
    <div class="col-1">{{user.username}}</div>
    <div class="col-2">{{user.email}}</div>
    <div class="col-2">{{user.address.city}}</div>
    <div class="col-2">{{user.phone}}</div>
    <div class="col-1">{{user.website}}</div>
    <div class="col-1" @click="$emit('del-user',user.id)" ><a  class="red" href="#">delete</a></div>
    <div class="col-1"><a   v-on:click="showeditform" class="blue">Edit</a></div>
</div>
<div class="row bg-secondary"  v-if="!editseen">
  <div class="col-12 mar">
   
    <form  @submit="usereditform">
       <h1 id="editform" class="text-center text-white">Edit User</h1>
       <span class="left" v-on:click="hideeditform">X</span>
        <input type="text" v-model="user.name" name="name" placeholder="name"><br>
        <input type="text" v-model="user.username" name="username" placeholder="username"><br>
         <input type="text" v-model="user.email" name="email" placeholder="email"><br>
        <input type="text" v-model="user.address.city" name="address" placeholder="address"><br>
        <input type="text" v-model="user.phone" name="phone" placeholder="phone_no"><br>
        <input type="text" v-model="user.website" name="website" placeholder="website"><br>
         <button type="submit" class="button" name="submit1">Submit</button>
        </form> 
  </div> 
 </div>
</div>
</template>

<script>

export default {
  name: 'viewsingleuser',
  props:['user'],
  data(){
    return {
          
      editseen:true
    }
  },
  methods:{
    showeditform(){
      this.editseen=false;
    },
    hideeditform(){
      this.editseen=true;
    },
     usereditform(e){
            e.preventDefault();
            const existuser={
                id:this.user.id,
                name:this.user.name,
                address:{city:this.user.address.city},
                username:this.user.username,
                email:this.user.email,
                phone:this.user.phone,
                website:this.user.website   
            }
            this.editseen=true;
            this.$emit('edit-user',existuser)
        }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.red{
    color: red;
}
.blue{
    color:blue;
}

input[type=text], select {
  width: 50%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=submit] {
  width:50%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit]:hover {
  background-color: #45a049;
}

form{
  position: relative;
  
}

.left{
  position: absolute;
  right:3rem;
  top:-0.8rem;
  color: red;
  cursor: pointer;
  font: 2rem sans-serif;
 text-align: left;
}
.mar{
  margin: 2rem;
  
}

</style>
