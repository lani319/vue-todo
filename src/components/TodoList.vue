<template>
  <div>
    <transition-group name="list" tag="ul"> <!-- css 클래스 연관 트랜지션 -->
        
            <li v-for="(todoItem,index) in propsdata" :key="todoItem.item" class="shadow">
                <i class = "checkBtn fas fa-check" 
                :class="{checkBtnCompleted : todoItem.completed}" @click="toggleComplete(todoItem,index)"></i>
                <span :class="{textCompleted : todoItem.completed}">
                {{todoItem.item}}
                </span>

                <span v-on:click="removeTodo(todoItem,index)">
                    <i class="fas fa-trash-alt"></i>
                </span>
            
            </li>
    </transition-group>
  </div>
</template>

<script>

export default {
    props: ['propsdata'],
    methods: {
        removeTodo (todoItem, index){            
            //localStorage.removeItem(todoItem);
            //this.todoItems.splice(index,1);
            this.$emit("removeTodoItem",todoItem,index);

        },
        toggleComplete (todoItem,index){
            
            
            
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

/* 리스트 아이템 트랜지션 효과 */

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>