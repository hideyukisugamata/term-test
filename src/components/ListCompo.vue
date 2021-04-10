<template>
  <div id="ListCompo">
      <div class="List-component" v-for="(value,index) in ExistLists" :key="index">
        <div class="flex">
          <input 
            type="text" 
            class="list-input"
            v-model="value.data.list"
            />
          <div class="list-button">
            <div class="update"  @click="Update(index)">
              <button class="update-button">更新</button>
            </div>
            <div class="delete" @click="Delete(index)">
              <button class="delete-button">削除</button>
            </div>
          </div>
        </div>
      </div>
  </div>
  
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
      ExistLists:[],
    }
  },
  methods:{
    async GetLists(){
      let data=[];
      const ExistLists = await axios.get("https://arcane-temple-90375.herokuapp.com/api/todos");
      for(let i = 0; i < ExistLists.data.data.length;i++){
      await axios
        .get("https://arcane-temple-90375.herokuapp.com/api/todos/" + ExistLists.data.data[i].id)
        .then((response)=>{
        data.push(response.data);
        console.log(data[i].data.list);
        })
      }
      this.ExistLists = data;
      console.log(ExistLists);
      
      
    },
    async Update(index){
      axios
        .put("https://arcane-temple-90375.herokuapp.com/api/todos/"+this.ExistLists[index].data.id,{
           list:this.ExistLists[index].data.list
        })
        .then((response)=>{
          console.log(response);
          this.$router.go({
            path:this.$router.currentRoute.path,
            force:true,
          });
        });
    },

    Delete(index){
      axios
        .delete("https://arcane-temple-90375.herokuapp.com/api/todos/"+this.ExistLists[index].data.id)
        .then((response)=>{
          console.log(response);
          this.$router.go({
            path:this.$router.currentRoute.path,
            force:true,
          });
        });
    },

  },
  created(){
    this.GetLists();
  },
  
};
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