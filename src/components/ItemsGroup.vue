<template>
<div>
<div>
  <h1>Jquery To Do List</h1>
</div>
<div>
  <h3>Simple Todo List with adding and filter by diff status.</h3>
</div>
<div>
  <div>
     <input type="text" v-model="num">
    <button @click="addItem" >Add</button>
    <div v-for="(el, index) in showItems" :key="index">
      <span>{{index+1}}.</span>
       <input type="checkbox" @click="selecetdItem(index)"/>{{el}}
    </div>
  </div>
  <div>
    <button >ALL</button>
    <button @click="showItems()">Active</button>
    <button >Complete</button>
  </div>
</div>

</div>
</template>

<script>
export default {
 name: 'ItemsGroup',
 data(){
    return {
      num:0,
      allItems: [],
      showItems: []
    }
  },
  methods:{
   addItem(){
     item = {val:num,isSelected:false}
     this.allItems.push(item)
     this.showItems.push(item)
   },
   selecetdItem(index){
    this.selectedItems[index].isSelected = true
   },
   showActivshowItemseItems(){
    this.showItems.filter(e=>(e.selecetdItem = false))
   }
}
}
</script>

<style scoped>
</style>
