<template>
  <div class="card">
    <h1>{{ msg }}</h1>
    <div class="card border-dark mb-3" id="info" v-if="state === true">
    <label for="todo-list" style="font-size:25px;">Create a new todo list</label>
    
    <label for="todo-list">Enter your name</label>
    <input type="text" placeholder="first name" v-model="name" style="margin-bottom:5%;">

    <label for="todo-list">Enter today's date</label>
    <input type="date" v-model="date" style="margin-bottom:15%;">
    
    <button class="btn btn-primary" :disabled="name.length === 0 && date.length === 0" @click="changeState()">create</button>
    
    </div>

    <div class="card border-dark mb-3" id="info" v-else-if="state === false">
      <h2  style="font-size:26px;">
        Welcome {{ name }}
      </h2>
    <p> Date : {{ date }}</p>

    <div style="margin-bottom:10%">
    <input type="text" placeholder="Add things to do" v-model="itemAdd" @keyup.enter="add">
    <button @click="add()" :disabled="itemAdd.length === 0" >ADD</button>
    </div>
    <div :class="{strikeout: item.done}" id="dam" v-for= "item in items" :key="item.id" style="text-align:left;">
    <input type="checkbox"  @change="toggle(item)">{{ " " + item.label }}
    <label id="fail" @click="del(item)">x</label>
    </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      checkcat: [],
      msg: 'Todo-list',
      name:'',
      date:'',
      state:true,
      itemAdd:'',
      complete:false,
      items:[
      ]
    }
  },
  methods: {
    changeState: function(){
      this.state = !this.state
    },
    add: function(){
      this.items.push({
        label:this.itemAdd,
        done:false
      })
      this.itemAdd=''
    },
    toggle: function(item){
      item.done=!item.done
    },
    del:function(item){
      this.items.splice( this.items.indexOf(item), 1 );
    }
  }
}
</script>

<style>
.strikeout {
    text-decoration: line-through;
    color: #B8C2CC;
}
.card{
  background-color: antiquewhite;
  margin-left: 25%;
  margin-right: 25%;
  padding-bottom: 3%;
}

h1{
  font-family: 'Times New Roman', Times, serif;
  font-size: 50px;
  padding-top: 2%;
}

#info{
  background-color: cornsilk;
  padding: 4%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.2);
}
#dam{
  text-decoration: none;
  display: block;
  font-size: 20px;
}

ul li:hover{
  cursor: pointer;
}

label{
  font: 20px;
}

#fail{
  width: 10px;
  height: 10px;
  color:red;
  margin-left: 5%
}
</style>
