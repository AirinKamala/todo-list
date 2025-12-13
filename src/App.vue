<template>
  <CountDown />
</template>
<script>
import CountDown from './components/CountDown.vue';
import StopWatch from './components/StopWatch.vue';
import TodoList from './components/TodoList.vue';

  export default {
    name: 'App',
    components: {
      StopWatch,
      TodoList,
      CountDown

    }
  }
</script>