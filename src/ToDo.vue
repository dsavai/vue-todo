<template>
  <div id="app">
    <div class="ToDo">
      <img class="Logo" :src="logo" alt="Vue logo"/>
      <h1 class="ToDo-Header">Vue To Do</h1>
      <div class="ToDo-Container">
        <div class="ToDo-Content">

          <ToDoItem v-for="item in this.list"
                    :id="item.id"
                    :todo="item.todo"
                    :key="item.id"
          >
          </ToDoItem>



        </div>
        <input type="text" v-model="toDoItem" v-on:keyup.enter="createNewToDoItem"/>
        <div class="ToDo-Add" @click="createNewToDoItem()">+</div>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue'
import Logo from './assets/logo.png';

export default {
  name: 'to-do',
  components: {
    ToDoItem
  },
  data() {
      return {
          list: [
              {
                  'id': 0,
                  'todo': 'clean the house'
              },
              {
                  'id': 1,
                  'todo': 'buy milk'
              }
          ],
          toDoItem: '',
          logo: Logo
      }
  },

  methods: {

      createNewToDoItem() {
          this.list.push(
              {
                  'id': this.list.length,
                  'todo': this.toDoItem
              }
          );
          this.toDoItem = '';
      }

  },

  mounted() {
    this.$on('delete', (event) => {
        this.list = this.list.filter(item => item.todo !== event)
    })
  }
}
</script>

<style>

  body {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    background: linear-gradient(#aeffae, #3d99ff);
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .Logo {
    width: 50px;
    position: relative;
    top: 50px;
  }

  .ToDo {
    text-align: center;
    border: 1px solid white;
    width: 80vw;
    height: 80vh;
    box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
    background: #f6f6f6;
  }

  .ToDo-Header {
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    font-weight: 400;
    text-transform: uppercase;
    margin: 70px auto 30px;
  }

  .ToDo-Add {
    color: white;
    font-size: 2em;
    width: 0.5em;
    height: 0.5em;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    cursor: pointer;
    background: #73ff73;
    border-radius: 10px;
    box-shadow: 1px 1px 1px #47a947;
    margin: 20px auto 0;
  }

  .ToDo-Add:hover {
    box-shadow: none;
    margin-top: 21px;
    margin-left: calc(auto + 1px);
  }

  .ToDo-Container {
    width: 80%;
    margin: 0 auto;
  }

  input {
    width: 60%;
    padding: 10px;
    font-size: 1em;
    margin: 10px auto;
    box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3)
  }
</style>
