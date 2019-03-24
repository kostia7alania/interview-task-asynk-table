<template>

<table  class="table table-striped table-bordered table-hover table-responsive">
  <thead>
    <tr>
      <th>#</th>
      <th  :class="{active: h==sortColumn}" class="table__header_click" scope="col" v-for="h in db_headers" :key="h" @click="sortHandler(h)">
        <span class="table-head-td"
       
        >
        <i v-if="h!=sortColumn" class="fas fa-sort"></i>
        <i v-else-if="h==sortColumn && type" class="fas fa-sort-amount-up"></i>
        <i v-else class="fas fa-sort-amount-down"></i>
        {{h}}
        </span>
      </th>
    </tr>
  </thead>
  <tbody> 
    <tr v-for="(obj, i) in db_comp" :key="i">
      <th scope="row">{{i}}</th>
      <td v-for="h in db_headers" :key="h">
         {{obj[h]}} 
      </td>
    </tr>
  </tbody>
</table>


</template>

<script> 

  export default {
    props: {
      db: Array,
      name: String,
    },
    data() {
      return {
        sortColumn: '',
        type: 0,
      }
    },
    watch: {
      name(neww,old){
        if(neww!=old) this.sortColumn = '';
        console.log('name changed', 'neww=>', neww, 'old=>',old)
      }
    },
    computed: {
      db_headers() {
        return this.db.length>0?Object.keys(this.db[0]):[];
      },
      db_comp () {
        if(this.sortColumn == "") return this.db
        const asc = (a, b) => a > b ? 1 : a < b ? -1 : 0;
        const desc = (a, b) =>  a > b ? 1 : a < b ? -1 : 0;
        return this.type
          ? this.db.sort((a, b) => asc(a[this.sortColumn], b[this.sortColumn]))
          : this.db.sort((a, b) => desc(b[this.sortColumn], a[this.sortColumn]));
      
      }
    },
    methods: {
      sortHandler(name) {
        if(this.sortColumn==name) {
          this.type = !this.type;
          return;
        }
        this.sortColumn = name;
      }
    }
  }
</script>


<style lang="scss" scoped>
  .table__header_click {
    
    transition: .5s;
    cursor: pointer;
    
    &:hover {
      color: red;
    }
  }
.table-head-td{
    width: max-content;
  }

  .active  {
    background:  rgba(187, 158, 158, 0.342);
    color: gray; 
  }
</style>