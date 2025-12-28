<template>
  <!-- <navbar>
    <ul>
      <button @click="currentView = 'TodoList'">Todo List</button>
      <button @click="currentView = 'StopWatch'">Stopwatch</button>
      <button @click="currentView = 'CountDown'">CountDown</button>
    </ul>
  </navbar>

  <div id="container">
    <div v-if="currentView == 'TodoList'">
      <TodoList />
    </div>

    <div v-else-if="currentView == 'StopWatch'">
      <StopWatch />
    </div>

    <div v-else-if="currentView == 'CountDown'">
      <CountDown />
    </div>
  </div> -->
<NoteTaker />
</template>

<style lang="scss">
navbar {
  width: 100vw;
  height: auto;
  

  button {
    background-color: transparent;
    border: none;
    border: solid 2px transparent;
    color: white;

    &:focus {
      outline: none;
    }

    &:hover {
      background-color: transparent;
      border: solid 2px transparent;
      border-top: solid 2px #646cff;
      border-right: solid 2px #646cff;

    }
  }
}

#container {
  border-radius: 2%;
  padding:20px;
  transform: translateY(-20px);
  padding-top: 0;
  border-top: solid 2px #646cff;
  border-right: solid 2px #646cff;

}
</style>
<script>
import CountDown from './components/CountDown.vue';
import NoteTaker from './components/NoteTaker.vue';
import StopWatch from './components/StopWatch.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    StopWatch,
    TodoList,
    CountDown,
    NoteTaker

  },
  data() {
    return {
      currentView: 'TodoList'
    }
  }
}
</script>