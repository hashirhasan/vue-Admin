<template>
  <div  v-if='!seen'>
      
    <form  @submit="adduser">
      <h1 class="text-center">Create User</h1>
        <span class="left" v-on:click="hideform">X</span>
        <input type="text" v-model="name" name="name" placeholder="name"><br>
        <input type="text" v-model="username" name="username" placeholder="username"><br>
         <input type="text" v-model="email" name="email" placeholder="email"><br>
        <input type="text" v-model="address" name="address" placeholder="address"><br>
        <input type="text" v-model="phone_no" name="phone" placeholder="phone_no"><br>
        <input type="text" v-model="website" name="website" placeholder="website"><br>
         <button  type="submit" class="button"  name="submit">Submit</button>
        </form>  
  </div>
</template>


<script>
 import { uuid } from 'vue-uuid';

export default {
    name:'adduser',
    data(){
        return {
            name:'',
            username:'',
            address:'',
            phone_no:'',
            email:'',
            website:'',
            isshow:true
        }
    },
    props:{
     seen: Boolean,
    },
 
    methods:{
      
     
      
        adduser(e){
            e.preventDefault();
            const newuser={
                 id:uuid.v4(),
                name:this.name,
                address:{city:this.address},
                username:this.username,
                email:this.email,
                phone:this.phone_no,
                website:this.website
            }
            this.$emit('add-user',newuser);
            this.name=""
            this.address=""
            this.username=""
            this.email=""
            this.phone_no=""
            this.website=""
        },
         hideform() {
          
      this.$emit('send-seen',this.isshow);
    },
    }

}
</script>

<style scoped>

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

div {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 40px 20px;
}
form{
  position: relative;
}
.left{
  position: absolute;
  right:2rem;
  top:-0.8rem;
  color: red;
  cursor: pointer;
  font: 2rem sans-serif;
 text-align: left;
}

</style>