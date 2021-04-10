<template>
<div id="app">
  <div class="window">
    <p>Todo List</p>
    <div class="flex">
      <input type="text" v-model="Newlist"/>
      <div class="add">
        <button class="add-button" @click="Newadd">追加</button>
      </div>
    </div>
    <list-compo/>
  </div>
</div>
</template>

<script>
import ListCompo from '../components/ListCompo.vue';
import axios from "axios";
export default{
  components:{
    ListCompo
  },
  data(){
    return{
      Newlist:"",
    };
  },
  methods:{
    Newadd(){
      axios
        .post('https://arcane-temple-90375.herokuapp.com/api/todos',{
          list:this.Newlist
        })
        .then(response=>{
          console.log(response);
          this.$router.go({
            path: this.$router.currentRoute.path,
            force: true,})
          this.Newlist="";
        })
    }
  }
};
</script>

<style scoped>
.window{
  height:auto;
  width:50%;
  background: #FFFFFF;
  padding:30px;
  border-radius: 15px;
  position: absolute;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
}
.window p{
  font-size:25px;
  font-weight:bold;
  margin-bottom: 15px;
}
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
.add,
.update,
.delete{
  margin: 2px 2px 2px 5px;
  height: 35px;
}
.add-button{
  color:#f995f8;
  border-color: #f995f8;
}
.add-button:hover{
  background:#f995f8;
  color:white;
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