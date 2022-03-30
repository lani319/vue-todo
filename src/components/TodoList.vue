<template>
  <div>

      <ul>
          <li v-for="(todoItem,index) in propsdata" v-bind:key="todoItem.item" class="shadow">
<i class = "checkBtn fas fa-check" v-bind:class="{checkBtnCompleted : todoItem.completed}" @click="toggleComplete(todoItem,index)"></i>
              <span v-bind:class="{textCompleted : todoItem.completed}">
              {{todoItem.item}}
              </span>

              <span v-on:click="removeTodo(todoItem,index)">
                 <i class="fas fa-trash-alt"></i>
              </span>
        
          </li>

      </ul> 
  </div>
</template>

<script>

export default {
    props: ['propsdata'],
    methods: {
        removeTodo : function(todoItem, index){            
            //localStorage.removeItem(todoItem);
            //this.todoItems.splice(index,1);
            this.$emit("removeTodoItem",todoItem,index);

        },
        toggleComplete : function(todoItem,index){
            
            
            
            this.$emit("todoCompleteEmit",todoItem,index);
            //로컬 스토리지 데이터 갱신 부분 
            //todoItem.completed = !todoItem.completed;
           // localStorage.removeItem(todoItem);
           // localStorage.setItem(todoItem.item,JSON.stringify(todoItem));

        }
    },

}
</script>

<style scoped>
.textCompleted {
    color: blue;
    text-decoration: line-through;

}
.checkBtnCompleted {
    color : red;
}
.checkBtn {
    line-height: 45px;
    color: cadetblue;
    margin-right: 5px;
}
.removeBtn {
    margin-left: auto;
    color: red;
}
</style>