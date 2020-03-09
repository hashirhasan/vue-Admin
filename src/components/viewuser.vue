<template>
<div class="p-2">
  <div class="row">
  
    <div class="font-weight-bold col-2">Name</div>
    <div class="font-weight-bold col-1">Username</div>
    <div class="font-weight-bold col-2">Email</div>
    <div class="font-weight-bold col-2">Address</div>
    <div class="font-weight-bold col-2">Phone No</div>
    <div class="font-weight-bold col-1">Website</div>
    <div class="font-weight-bold col-1">DELETE</div>
    <div class="font-weight-bold col-1">EDIT</div>
  </div>
   <viewsingleuser v-bind:key="user.id" v-for="user in users" v-bind:user="user"  v-on:del-user="$emit('del-user',user.id)" v-on:edit-user="editinguser" />

  </div>
</template>

<script>
import viewsingleuser from './viewsingleuser.vue'
export default {
  name: 'viewuser',
  components:{
      viewsingleuser
  },
  props:['users'],
  data(){
    return {
      existuser:''
    }
  },
  methods:{
    editinguser(existuser)
    {
      this.existuser=existuser;
       this.$emit('edit-user',this.existuser)
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
div{
  word-wrap :break-word;
  padding: 0.8rem;
}

</style>
