<template>
  <div>
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem" ></TodoInput>
    <!--
      v-on:하위컴포넌트 이벤트 이른 = "현재컴포넌트 메쏘드 이름"
      -->
    <TodoList v-bind:propsdata='todoItems' 
    v-on:removeTodoItem="removeTodo" 
    v-on:todoCompleteEmit="todoComplete"></TodoList>
    <TodoFooter v-on:clearAllTodoEmit="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'


export default {

data() {
    return {
        todoItems : [] //completed : , item : 
    }
},
//리스트 가져오기 
created  () {    
    if(localStorage.length > 0){
        for(let i = 0; i < localStorage.length ; i++){
            if(localStorage.key(i) != ""){                
                //console.log( JSON.parse(localStorage.getItem(localStorage.key(i))));
                this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            }
        }
    }
},
methods : {
  addOneItem  (todoItem){
          const obj = {completed:false, item : todoItem};
            //저장하는 로직             
            localStorage.setItem(todoItem, JSON.stringify(obj));
            this.todoItems.push(obj);        
        },
  removeTodo (todoItem, index){         
    //console.log("remove")   
            localStorage.removeItem(todoItem.item); //삭제는 객체를 지우면 안되고, 객체의 키 값을 지워야 한다. 그래서 .item을 넣는다. 
            this.todoItems.splice(index,1);

        },
  todoComplete (todoItem,index){
     //console.log(index);
     //todoItem.completed = !todoItem.completed;
     this.todoItems[index].completed = !this.todoItems[index].completed;
     //로컬 스토리지 데이터 갱신 부분 
     localStorage.removeItem(todoItem.item);
     localStorage.setItem(todoItem.item,JSON.stringify(todoItem));
  },
  clearAll  (){
    localStorage.clear();
    this.todoItems = [];
  }
},
components : {
  TodoHeader,
  TodoInput,
  TodoList,
  TodoFooter
}

}

</script>



<style>
body {
  text-align: center;
  background-color: #f6f6f6;

}

input {
  border-style: groove;
  width : 200px;
}
button {
  border-style: groove;
}
.shadow{
  box-shadow: 5px 10px  10px rgba(0,0,0,0.03);
}
</style>