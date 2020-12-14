<template>
  <div class="user-profile">
      <div class="user-profile_user-panel">
          <h1 class="user-profile_username">{{user.username}}</h1>
          <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
          <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{followers}}
          </div>
          <form class="user-profile_create-todo" @submit.prevent="createNewTodo">
              <label for="newTodo"><strong>New Todo</strong></label>
              <textarea name="" id="newTodo" cols="30" rows="4" v-model="newTodoContent"/>

              <div class="user-profile_create-todo-type">
                  <label for="newTodoType"><strong>Type: </strong></label>
                  <select id="newTodoType" v-model="selectedTodoType">
                      <option :value="option.value" v-for="(option, index) in todoTypes" :key="index"> {{option.name}}</option>
                  </select>
              </div>
              <button>
                  Add Todo!
              </button>
          </form> 
      </div>
      <div class="user-profile_todos-wrapper">
          <TodoItem v-for="todo in user.todos" :key="todo.id" :username="user.username" :todo="todo" @important="toggleImportant" />
      </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
  name: 'UserProfile',
  components:{TodoItem},
  data(){
    return {
    newTodoContent: '',
    selectedTodoType: 'instant',
    todoTypes:[
          {value: 'draft', name:'Draft'},
          {value: 'instant', name:'Instant Todo'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'atidivya',
        firstName: 'Atidivya',
        lastName: 'Patra',
        email: 'atidivya@gmail.com',
        isAdmin: true,
        todos: [
            {id:1, content: 'todo is amazing!'},
            {id:2, content: 'fix wall!'}
        ]
      }
    }
  },
  watch:{
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  computed: {
    fullName(){
      return `${this.user.firstName} ${this.user.lastName} `;
    }
  },
  methods:{
    followUser(){
      this.followers++
    },
    toggleImportant(id){
        console.log(`Important todo #${id}`)
    },
    createNewTodo(){
        if(this.newTodoContent && this.selectedTodoType !== 'draft'){
            this.user.todos.unshift({
                id:this.user.todos.length + 1,
                content: this.newTodoContent
            })
            this.newTodoContent = '';
        }
    }
  },
  mounted(){
    this.followUser();
  }
}
</script>

<style>
   .user-profile {
       display: grid;
       grid-template-columns: 1fr 3fr;
       width: 100%;
       padding: 50px 5%;
   }

   .user-profile_user-panel {
       display: flex;
       flex-direction: column;
       margin-right: 50px;
       padding: 20px;
       background-color: white;
       border-radius: 5px;
       border: 1px solid #dfe3e8;
   }

   .user-profile_admin-badge {
       background: rebeccapurple;
       color: white;
       border-radius: 5px;
       margin-right: auto;
       padding: 0 10px;
       font-weight: bold;
   }

   h1{
       margin: 0;
   }

   .user-profile_todos-wrapper {
       display: grid;
       grid-gap: 10px;
   }

   .user-profile_create-todo {
       padding-top: 20px;
       display: flex;
       flex-direction: column;
   }
</style>