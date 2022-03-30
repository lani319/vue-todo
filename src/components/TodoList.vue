<template>
  <div>

      <ul>
          <li v-for="(todoItem,index) in todoItems" v-bind:key="todoItem.item" class="shadow">
<i class = "checkBtn fas fa-check" v-bind:class="{checkBtnCompoleted : todoItem.completed}" @click="toggleComplete(todoItem,index)"></i>
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
data : function() {
    return {
        todoItems : [] //completed : , item : 
    }
},
methods : {
    removeTodo : function(todoItem, index){
        console.log(todoItem,index);
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index,1);

    },
    toggleComplete : function(todoItem,index){
        console.log(todoItem,index);
        todoItem.completed = !todoItem.completed;
        
        //로컬 스토리지 데이터 갱신 부분 
        localStorage.removeItem(todoItem);
        localStorage.setItem(todoItem.item,JSON.stringify(todoItem));

    }
},
created : function() {
    if(localStorage.length > 0){
        for(var i = 0; i < localStorage.length ; i++){
            if(localStorage.key(i) != ""){                
                //console.log( JSON.parse(localStorage.getItem(localStorage.key(i))));
                this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            }
        }
    }
}
}
</script>

<style scopped>
.textCompleted {
    color: blue;
    text-decoration: line-through;

}
.checkBtnCompoleted {
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