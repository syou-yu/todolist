<template>
  <div id="edit">

    <div class="addTodo">
        <el-input class="input" v-model="editMessage[0]" @keyup.enter="edit_success" >
        <el-button slot="append" @click="edit_success">确定</el-button>
    </el-input>
  </div>
  </div>
</template>

<script>
export default {
    props:['editMessage'],
    methods:{
        edit_success(){
            if(this.editMessage){
                this.$emit('edit',this.editMessage);
            }else{
                alert('内容不能为空');
            }
        }
    }
}
</script>

<style scoped>

</style>
