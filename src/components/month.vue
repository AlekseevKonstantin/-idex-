<template>
  <div class="month">
    <week v-for="(days,i) in weeksArray" 
          v-bind:key="i" 
          v-bind:days="days"
          v-bind:year="year"
          v-bind:month="month"
          v-bind:user="user">
    </week>
  </div>
</template>

<script>
  import Week from './week'

  export default {
    props: {
      year: Number,
      month: Number,
      user: Object
    },
    data(){
      return {
        weeks: undefined,
        lweek: undefined,
        fweek: undefined,
        weeksArray: []
      }
    },
    methods: {
      countDays(year, month){
        return new Date(year, month, 0).getDate();
      },
      countWeeks(year, month) {
        let weeks = 1;
        let day = -1;
        let countDays = this.countDays(year, month+1);
        let fday = new Date(year, month, 1).getDay();
        let lday = undefined;

        for (let i = 1; i <= countDays; i++) {
          let newday = new Date(year, month, i).getDay();
          if (day == 0 && newday == 1) {
              weeks += 1;
          }
          day = newday;
        }

        lday = day;

        return {
          weeks,
          fday,
          lday 
        }
      }
    },
    created(){
      this.weeks = this.countWeeks(this.year, this.month);
      this.fweek = this.weeks.fday === 0 ? 1: 7-this.weeks.fday+1;
      let countDayOnLastWeek = 7-(7-this.weeks.lday);
      this.lweek = countDayOnLastWeek === 0 ? 7 : countDayOnLastWeek;

      let lastElement = 0;
      let dayIndex = 1;
      for(let i = 0; i < this.weeks.weeks; i += 1){
        
        switch (i){
          case 0:
            lastElement = this.fweek;
            break;
          case this.weeks.weeks-1:
            lastElement = this.lweek;
            break;
          default:
            lastElement = 7;
            break;    
        }
        let days = []
        for(let j = 0; j < lastElement; j += 1){
          days[j] = dayIndex;
          dayIndex += 1;
        }

        this.weeksArray[i] = days;
      }
    },
    components:{
      Week
    }

  }
</script>

<style lang="scss">
  .month{
    position: relative;
    display: flex;
  }
</style>