<template>
  <div class="clearAllContainer">
        
    <span class="clearAllBtn" @click="clearAll">
    Clear All  
    </span>
    </div>
</template>

<script>
export default {

  methods : {
    clearAll : function(){
      localStorage.clear(); 
    }
  }

}
</script>

<style scoped>

.clearAllContainer {
  width : 8.5rem;
  height : 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 0 auto;
}
.clearAllBtn{
  color: red;
  display: block;
}

</style>