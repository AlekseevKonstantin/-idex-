<template>
  <div class="week">
    <day v-for="(day,i) in days" 
         v-bind:key="i"
         v-bind:year="year"
         v-bind:month="month"
         v-bind:day="day"
         v-bind:user="user">
    </day>
  </div>
</template>

<script>
  import Day from './day';

  export default {
    props:{
      days: Array,
      year: Number,
      month: Number,
      user: Object
    },
    
    components:{
      Day
    } 
  }
</script>

<style lang="scss">
  .week{
    margin-left: 2px;
  }

  .week:first-child{
    margin-left: 0;
    align-self: flex-end;
  }
</style>