<template>
<div>
  <Card class="div-card">
  <ListHeader></ListHeader>
<div class="div-body">
   <Input class="div-body-input" type="text" v-model="$store.state.itemName"></Input>
   <Button type="success" class="div-body-add-button"    @click="addItem" >Add</Button>
    <div class="div-body-data-table">
      <div class="div-body-data-table-outer">
    <div  class="div-body-data-table-single" v-for="(el, index) in $store.state.showItems" :key="index" > 
         <Item  :index="index"></Item>
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
      status: 'All'
    }
  },
  methods:{
   addItem(){
     if(this.$store.state.itemName != ""){
       let item = {
       val:this.$store.state.itemName,
       isSelected: this.status =='Complete'?true:false,
       isEditing: false
       }
     this.$store.commit('pushItem',item)
     this.$store.commit('resetItemName')
     }else{
        this.$Message.error('Can not add a null item')
     }
   },
   showItemsStatus(status){
     this.status = status
     if(status=='Active'){
        this.$store.commit('filterItems','Active')
     }else if(status=='Complete'){
        this.$store.commit('filterItems','Complete')
     }else{
       this.$store.commit('getAllItems')
     }
   },
}
}
</script>
