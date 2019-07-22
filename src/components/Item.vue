<template>
      <div  v-bind:class="{'div-body-data-item':itemData.index % 2 == 0}">
         <span  class="div-body-data-table-del" v-if="itemData.el.isSelected">{{itemData.index+1}}.</span>
      <span v-else>{{itemData.index+1}}. </span> 
      <span>
         <Checkbox size="large" class="div-body-data-table-checkbox" @click="completedItem(itemData.index)" v-model="itemData.el.isSelected">  </Checkbox>
         <span v-if="!itemData.el.isEditing" @dblclick="editItemName(itemData.index)">
          <del v-if="itemData.el.isSelected" class="div-body-data-table-del" >{{itemData.el.val}}</del>
        <span v-else>{{itemData.el.val}}</span>  
         </span>
       <Input v-else v-model="itemData.el.val" :autofocus="true" class="div-body-data-table-input" size="small" @on-blur="itemInputOnBlur(itemData.index)" @on-enter="itemInputOnBlur(itemData.index)"></Input>
       </span>
      </div>
</template>
<script>
export default {
  name: 'Item',
props:['itemData'],
data(){
    return {
     
    }
  },
 methods:{
    completedItem(index){
     this.$emit("completedItem",index)
   },
   editItemName(index) {
      this.$emit("editItemName",index)
   },
   itemInputOnBlur(index) {
      this.$emit("itemInputOnBlur",index)
   }
 }
}
</script>


