<template>
  <div class="item">
    <p>Nowe todo: {{newItem}}</p>
    <input type="text" placeholder="todo" v-model="newItem"/>
    <button @click="addItem">Dodaj zadanie</button>
  </div>

  <div 
    class="item"
    v-bind:class="{
      completed: item.completed
    }"  
    v-for="item in items" 
    v-bind:key="item.id"
  >
    <h2>{{item.title}}</h2>
    <button v-if="!item.completed" @click="removeItem(item.id)">Zakończone</button>
  </div>
</template>

<script>

export default {
  data(){
    return {
      newItem:'',
      items: [
      {title: 'Zrobić zakupy', completed: false, id: 1},
      {title: 'Kupić prezent', completed: false, id: 2}
      ]
    }
  },
  methods:{
    addItem(){
      this.items.push({title: this.newItem, completed: false, id: Math.random()})
      this.newItem =''
    },
    removeItem(id){
      const index = this.items.findIndex(el => el.id === id);
      this.items[index].completed = true;
      
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.item{
  border: 1px solid #cdcdcd;
  margin: 8px;
  padding: 10px;
}
.completed{
  opacity: 0.5;

}
.completed h2{
  text-decoration: line-through;
}
</style>
