<template>
 <div id="app" class="container">
      <Header  /> 
      <div >
        <div v-if="isseen">
      <button class='button'  v-on:click="showform" >Add post</button> 
        </div>
        <div v-else>
            <button class='button'  v-on:click="hideform" >close</button> 
        </div>
       <addpost  v-on:add-post="addpost"   v-bind:seen="isseen"  v-on:send-seen="hideform"    />
      <viewpost v-bind:posts="posts" v-on:edit-post="editpost"  v-on:del-post="deletepost"/>
      </div>
   </div>

</template>


<script>
import  axios  from "axios";
import Header from './components/Header'
import viewpost from './components/viewpost'
import addpost from './components/addpost'
// import editpost from './components/editpost'
export default {
    name:'Admin',
    components:{
        Header,
        viewpost,
        addpost,
        
    },
 data(){
    return{
        posts:[],
        isseen:true,
        
    }
  },
  methods:{
    deletepost(id){
      this.$swal.fire({
  title: 'Are you sure?',
  text: "You won't be able to revert this!",
  icon: 'warning',
  showCancelButton: true,
  confirmButtonColor: '#3085d6',
  cancelButtonColor: '#d33',
  confirmButtonText: 'Yes, delete it!'
}).then((result) => {
  if (result.value) {
     this.posts=this.posts.filter(post=> post.id!==id);
   this.$swal.fire(
      'Deleted!',
      'Your file has been deleted.',
      'success'
    )
  
  }
    
})
    
    },
    addpost(newpost)
    {
      this.$swal.fire(
        'Created!',
        'User has been created!',
        'success'
      )
      this.posts=[...this.posts,newpost];
    }, 
    showform:function(event) {
        console.log(event)
      this.isseen = false
      console.log(this.isseen)
    },
    hidenform()
    {
     this.isseen=true;
    },
    hideform(isshow)
    {
      this.isseen=isshow;
      console.log(isshow)
    },
    editpost(existpost){
      this.$swal.fire(
        'Updated!',
        'User details have been updated!',
        'success'
      )
      this.posts=this.posts.filter(post=> post.id!==existpost.id)
       this.posts=[...this.posts,existpost];
    }
   
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/users')
    .then(res=> this.posts=res.data)
    .catch(err=> console.log(err))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top:0px;
  padding-bottom:10rem;
}


table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}
.button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  width:25%;
  border-radius:15px;
  outline:none;
}
.button:hover{
  background-color:green
}

.space{
    margin:20px;
}
.row {
  font-size: 0.8rem;
  border-bottom: 1px solid black;
 
}
a{
  cursor: pointer;
}

</style>