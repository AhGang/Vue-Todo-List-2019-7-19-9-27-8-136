<template>
<div>
  <Card class="div-card">
<div class="div-header">
  <div class="div-header-title">
  <h1>Jquery To Do List</h1>
</div>
<div class="div-header-comment">
  <h3>Simple Todo List with adding and filter by diff status.</h3>
</div>
</div>    
<div class="div-body">
     <Input class="div-body-input" type="text" v-model="itemName"></Input>
    <Button type="success" class="div-body-add-button"    @click="addItem" >Add</Button>
    <div class="div-body-data-table">
      <div class="div-body-data-table-outer">
    <div  class="div-body-data-table-single" v-for="(el, index) in showItems" :key="index" > 
         <Item :itemData="{el:el,index:index}" @completedItem="completedItem" @editItemName="editItemName" @itemInputOnBlur="itemInputOnBlur"></Item>
    </div>
      </div>
      </div> 
  </div>
  <div class="div-footer">
    <Button type="text" class="div-footer-button"  @click="showItemsStatus('All')">All</Button>
    <Button type="text" class="div-footer-button"  @click="showItemsStatus('Active')">Active</Button>
    <Button type="text" class="div-footer-button"  @click="showItemsStatus('Complete')">Complete</Button>
  </div>
  </Card>
</div>

</template>

<script>
import Item from './Item'
export default {
 name: 'ItemsGroup',
 components:{Item},
 data(){
    return {
      itemName:"",
      allItems: [],
      showItems: [],
      status: 'All'
    }
  },
  methods:{
   addItem(){
     if(this.itemName != ""){
       let item = {
       val:this.itemName,
       isSelected: this.status =='Complete'?true:false,
       isEditing: false
       }
     this.allItems.push(item)
     this.showItems.push(item)
     this.itemName = ""
     }else{
        this.$Message.error('Can not add a null item')
     }
   },
   showItemsStatus(status){
     this.status = status
     if(status=='Active'){
        this.showItems = this.allItems.filter(e=>(e.isSelected == false))
     }else if(status=='Complete'){
        this.showItems = this.allItems.filter(e=>(e.isSelected == true))
     }else{
       this.showItems = JSON.parse(JSON.stringify(this.allItems))
     }
   },
    completedItem(index){
     if(!this.showItems[index].isSelected){
      this.showItems[index].isSelected = true
      this.allItems[index].isSelected = true
     }else{
      this.showItems[index].isSelected = false
      this.allItems[index].isSelected = false
     }
   },
   editItemName(index) {
      this.showItems[index].isEditing = true;
   },
   itemInputOnBlur(index) {
      this.showItems[index].isEditing = false;
   }
}
}
</script>
