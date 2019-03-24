<template>
  <div id="app">
    <Jumbo @getPosts="getPosts"/>
    <Table :name="name" :db="db" />
  </div>
</template>

<script>
import Table from "@/components/Table";
import  Jumbo from "@/components/Jumbo";

export default {
  name: "app",
  data(){
    return {
      //url: 'http://localhost:3000/',
      url: 'https://jsonplaceholder.typicode.com',
      db: [],
      name: ''
    }
  },
  components: {
    Table,
    Jumbo
  },
  methods: {
    getPosts(name){
     fetch(`${this.url}/${name}`)
      .then(res=>res.json())
      .then(res=>{
        this.db = (res instanceof Array) ? res : this.db
        this.name = name;
      })
      .catch(err=>console.warn('err=>',err))
      
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
