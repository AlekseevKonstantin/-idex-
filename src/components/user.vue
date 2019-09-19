<template>
  <tr>
    <td>
      <p class="vs-app-user-info">
        <img v-bind:src="user.photo" alt="" class="vs-app-user-photo">
        <span class="vs-app-user-fio">
          <span class="vs-app-user-name">{{user.name}}</span> 
          <span class="vs-app-user-surname">{{user.surname}}</span>
        </span>
      </p>  
    </td>
    <td>
      <span class="vs-app-vacation-days">
        <span class="vs-app-number-past-days">{{countPastDays}}</span>
        <span class="vs-app-separator">/</span>
        <span class="vs-app-number-days">{{user.limitHolidays}}</span>
      </span>
    </td>

    <td v-for="i in months" v-bind:key="i">
      <month v-bind:year="year" 
             v-bind:month="i" 
             v-bind:key="year"
             v-bind:user="user">
      </month>
    </td>
  </tr>
</template>

<script>
import Month from './month'
  export default {
    props:{
      months: Array,
      year: Number,
      user: Object
    },
    data(){
      return{
        weeks: 0
        
      }
    },
    computed:{
      countPastDays(){
        if(this.user.holidays.length === 1){
          return this.user.holidays[0].count;
        }

        let sumCount = this.user.holidays.reduce((prevItem, item) => {
          let prevYear = new Date(Date.parse(prevItem.start)).getFullYear(),
              curYear = new Date(Date.parse(item.start)).getFullYear();

          if(prevYear === this.year && curYear === this.year){
            return prevItem.count + item.count
          }

          return 0;
        });
        return sumCount > this.user.allHoludaysCount ? this.user.allHoludaysCount : sumCount;
      }
    },
    components:{
      Month
    }    
  }
</script>

<style lang="scss">
  
  @mixin tbody-font {
    font-size: 12px;
    color: #232323;
  } 

  @mixin flex-align-center {
    display: flex;
    align-items: center;
  }

  @mixin flex-align-start { 
    display: flex;
    align-items: flex-start;
  }

  .vs-app-user-info{
    @include flex-align-center;
    margin: 0;
    padding: 10px 7px;
  }

  .vs-app-user-fio{
    @include tbody-font;
    @include flex-align-start;
    flex-direction: column;
    justify-content: flex-start;
    margin-left: 10px;
  }

  .vs-app-vacation-days{
    @include tbody-font;
  }

  .vs-app-user-photo{
    width: 32px;
    height: 32px;
  }

  
</style>