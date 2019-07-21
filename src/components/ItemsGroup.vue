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
      <span  class="div-body-data-table-del" v-if="el.isSelected">{{index+1}}.</span>
      <span v-else>{{index+1}}.</span> 
      <span>
         <Checkbox class="div-body-data-table-checkbox" @click="completedItem(index)" v-model="el.isSelected">  </Checkbox>
         <span v-if="!el.isEditing" @dblclick="editItemName(index)">
          <del v-if="el.isSelected" class="div-body-data-table-del" >{{el.val}}</del>
        <span v-else>{{el.val}}</span>  
         </span>
       <Input v-else v-model="el.val" :autofocus="true" class="div-body-data-table-input" size="small" @on-blur="itemInputOnBlur(index)" @on-enter="itemInputOnBlur(index)"></Input>
       </span>
  
     
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
export default {
 name: 'ItemsGroup',
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
   completedItem(index){
     if(!this.showItems[index].isSelected){
      this.showItems[index].isSelected = true
      this.allItems[index].isSelected = true
     }else{
      this.showItems[index].isSelected = false
      this.allItems[index].isSelected = false
     }
   },
   showItemsStatus(status){
     this.status = status
     if(status=='Active'){
        this.showItems = this.allItems.filter(e=>(e.isSelected == false))
     }else if(status=='Complete'){
        this.showItems = this.allItems.filter(e=>(e.isSelected == true))
     }else{
        this.showItems = this.allItems;
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
