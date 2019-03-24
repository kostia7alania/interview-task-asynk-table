
<template>
<div>
  <b-jumbotron header="Interview Test Task" lead="Async table">

    <b-container>
      <b-button :variant="variants[getRand()]" @click="getPosts(el)" v-for="el in btns" :key="el">{{el}}</b-button>
    </b-container>
  </b-jumbotron>
</div>

</template>

<script>
export default {
  name: 'jumbo',
  data(){return{
    btns: ['posts',  'comments',  'albums',  'photos',  'todos',  'users'],
    variants: ['primary','secondary',
'success',
'danger',
'warning',
'info',
'light',
'dark' ]
  }},

  methods: { 
    getPosts(name){this.$emit('getPosts',name)},
    randVar(){
      return this.variants[this.getRand()]
    },
    getRand: ()=>Math.round(Math.random() * (7- 0) + 0)
  }

}
</script>