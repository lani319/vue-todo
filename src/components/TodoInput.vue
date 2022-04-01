<template>
<div class="inputBox shadow">
  <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
  <!--
  <button class="addBtn" @click="addTodo">add</button>
  -->
  <span class="addContainer">
     <i class="fas fa-plus addBtn" @click="addTodo"></i>
  </span>
    <Modal v-if="showModal" @close="showModal = false">
        <!--
      you can use custom content here to overwrite
      default content
      <vslot="header">custom header</ㅅ>
    -->
        <div vslot = "header">
        경고!    
        </div>        
        <div vslot = "body">
        값 입력해주세요.
        </div>
        
      </Modal>

  </div>
</template>

<script>

import Modal from './common/AlertModal.vue';

export default {

    data () {
            return {
                newTodoItem : "",
                showModal : false,
            }
    },
    methods : {
        addTodo (){
            if(this.newTodoItem !== ''){
                this.$emit('addTodoItem',this.newTodoItem);
                //addTodoItem; app.vue로 올라간다. 파라미터는 input 텍스트 값 
                this.clearInput();
            }else{
                //여기에 모달을 띄운다. 
                this.showModal = !this.showModal;
                
            }
            
        },
        clearInput (){
            this.newTodoItem = "";
        },
        
    },
    components : {
        //인풋의 하위가 모달, 인풋의 상위가 앱.뷰 
        Modal
    }

}
</script>

<style scoped>
input:focus{
    outline : none;
}
.inputBox{
    background-color: #FFFFFF;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float : right;
    background: linear-gradient(to right,#6478fb,#8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color : #FFFFFF;
    vertical-align: middle;
}

</style>