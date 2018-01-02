<template>
  <div class="addTodo">
        <el-input class="add_input" v-model="todo" @keyup.enter="addTodo" >
          <el-button slot="append" @click="addTodo">添加</el-button>
        </el-input>
  </div>
</template>

<script>
export default{
    data(){
        return{
            todo:''
        }
    },
    methods:{
        addTodo(){
            if(this.todo){
                this.$emit('add',this.todo);
                this.todo = '';
                
            }else{
                this.$message({
                message: '内容不能为空',
                type: 'error'
                });
            }
        }
    }
}
</script>

<style scoped>
#addTodo{
    max-width: 300px;
}

</style>
