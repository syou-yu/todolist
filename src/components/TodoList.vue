<template>
  <div id="todoList">
        <h1>Todo List</h1>
        <ul class="todos">
            <li v-for="(todo,index) in todos" :key="index" class="todo">
                
                <el-checkbox v-model="todo.isCompleted" @click="completed(index)" class="todo_checkbox">
                    <!-- TodoList显示 -->
                    <span   
                    :class="todo.isCompleted ? 'completed' : ''"
                    @click="completed(index)">
                        {{todo.text}}
                    </span>
                    
                </el-checkbox>
                <!-- 操作按钮 -->
                <el-button-group class="btn-group">
                    <!-- 编辑按钮 -->
                    <el-button @click="edit(index)" icon="el-icon-edit"  size="mini" round ></el-button>
                    <!-- 删除按钮 -->
                     <el-button @click="del(index)" icon="el-icon-delete"  size="mini"  round></el-button>
                </el-button-group>                
            </li>
            
        </ul>
        <!-- 添加todo -->
        <add-todo @add="addTodo"></add-todo>
        <!-- 数据统计 -->
        <p v-show="this.todos.length===0">所有事项已完成！</p>
        <div v-show="this.todos.length!==0">
            <p>总共有 <strong>{{ this.todos.length }}</strong> 个待办事项。</p>
            <p><strong style="color:#409EFF;font-size:20px">{{ completedCounts }}</strong> 个已完成。</p>
            <p><strong style="color:#F56C6C;font-size:20px">{{ notcompletedCounts }}</strong> 个未完成。</p>
        </div>

        <el-dialog
        :visible.sync="showEdit"
        :show-close="false" 
        center
        title="修改待办事项"
        width="75%">
            <edit-todo   @edit="edit_success" :editMessage="this.editMessage"></edit-todo> 
        </el-dialog>  
        
  </div>
</template>

<script>
import addTodo from './addTodo'
import editTodo from './editTodo'
export default{
    components:{
        addTodo,
        editTodo
    },
    data(){
        return{
            todos:[
                {
                    text: '吃饭',
                    isCompleted:true
                },
                {
                    text:'睡觉',
                    isCompleted:false
                },
            ],
            editMessage:'',
            showEdit:false
        }
    },
    computed:{
        completedCounts () {
            return this.todos.filter(item => item.isCompleted).length
        },
        notcompletedCounts(){
            return this.todos.filter(item => !item.isCompleted).length
        },
    },
    methods:{
        completed(index){
            this.todos[index].isCompleted = !this.todos[index].isCompleted;
        },
        addTodo(todo){
            let add = {
                text:todo,
                isCompleted:false
            };
            this.todos.push(add);
            this.$message({
                message: '创建成功',
                type: 'success'
            });
        },
        edit(index){
            this.editMessage = [this.todos[index].text,index];
            this.showEdit = !this.showEdit;
        },
        edit_success(editMessage){
            let index = editMessage[1];
            this.todos[index].text = editMessage[0];
            this.editMessage = '';
            this.showEdit = !this.showEdit;
        },
        del(index){
            this.todos.splice(index,1);
            this.$message({
                message: '删除成功',
                type: 'success'
                });
        }
        
    }
}
</script>

<style scoped>
#todoList{
    margin:0 auto;
    max-width: 300px;
    
}
.todo{
    position: relative;
    text-align:left;
    cursor: pointer;
}
.todos li{
    list-style:none;
    margin: 5px 0;
}
.todos{
    margin-left:-25px;
}

.todo_checkbox span{
    font-family:Microsoft YaHei;
    font-size:18px;
    line-height: 30px;
}
.completed {
  text-decoration: line-through;
}
.btn-group{
    position  : absolute;
    top: 50%;
    right: 10px;
    transform : translate(0,-50%);
}
</style>
