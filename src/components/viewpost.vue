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
   <viewsinglepost v-bind:key="post.id" v-for="post in posts" v-bind:post="post"  v-on:del-post="$emit('del-post',post.id)" v-on:edit-post="editingpost" />

  </div>
</template>

<script>
import viewsinglepost from './viewsinglepost.vue'
export default {
  name: 'viewpost',
  components:{
      viewsinglepost
  },
  props:['posts'],
  data(){
    return {
      existpost:''
    }
  },
  methods:{
    editingpost(existpost)
    {
      this.existpost=existpost;
       this.$emit('edit-post',this.existpost)
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
