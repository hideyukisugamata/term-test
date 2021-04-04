<template>
  <div id="ListCompo">
      <div class="List-component" v-for="(value,index) in Existing" :key="index">
        <div class="flex">
          <input 
            type="text" 
            class="list-input"
            v-model="Existing">
          <div class="list-button">
            <div class="update">
              <button class="update-button">更新</button>
            </div>
            <div class="delete">
              <button class="delete-button">削除</button>
            </div>
          </div>
        </div>
      </div>
  </div>
  
</template>

<script>
export default {
  data(){
    return{
      Existing:[
        "sample1","sample2","sample3"]
    }
  }

}
</script>

<style>
.flex,
.list-button{
  display: flex;
  justify-content: space-between;
}
input{
  width:80%;
  height: 30px;
  border-radius: 5px;
  border: 2px solid #e5e3e3;
  margin-bottom:15px;
}
.list-input{
  width:30%;
}
button{
  height: 35px;
  width:60px;
  border-radius: 5px;
  font-size:12px;
  font-weight: bold;
  background-color: white;
  outline:none;
  border: 2.5px solid;
  cursor: pointer;
  transition: 1s;
}
.update,
.delete{
  margin: 2px 2px 2px 5px;
  height: 35px;
}
.update-button{
  color: #ffbe6b;
  border-color: #ffbe6b ;
}
.update-button:hover{
  background:#ffbe6b;
  color: white;
}
.delete-button{
  color: #8dfcef;
  border-color: #8dfcef ;
}
.delete-button:hover{
  background: #8dfcef;
  color: white;
}
</style>