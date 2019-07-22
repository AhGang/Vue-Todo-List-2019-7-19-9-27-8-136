<template>
<div>
  <Card class="div-card">
  <ListHeader></ListHeader>
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
  <ListFooter @showItemsStatus="showItemsStatus"></ListFooter>
  </Card>
</div>

</template>

<script>
import Item from './Item'
import ListHeader from './ListHeader'
import ListFooter from './ListFooter'
export default {
 name: 'ItemsGroup',
 components:{Item,ListHeader,ListFooter},
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
