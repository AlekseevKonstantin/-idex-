<template>
  <div class="vs-app">
    <header class="vs-app-header">
      <h2 class="vs-app-header__head">График отпусков</h2>

      <div class="vs-app-controlls">
        <a href="#" class="vs-app-left-controll" v-on:click.prevent="decYear"></a>
        <span class="vs-app-cur-year">{{curYear}}</span>
        <a href="#" class="vs-app-right-controll" v-on:click.prevent="incYear"></a>
      </div>
    </header>
    <div class="vs-app-table-wrapper">
      <table class="vs-app-table">
        <thead>
          <tr>
            <th class="vs-app-table-head">Фамилия, Имя</th>
            <th class="vs-app-table-head">дней</th>
            <th class="vs-app-table-head">Янв</th>
            <th class="vs-app-table-head">Фев</th>
            <th class="vs-app-table-head">Мар</th>
            <th class="vs-app-table-head">Апр</th>
            <th class="vs-app-table-head">Май</th>
            <th class="vs-app-table-head">Июн</th>
            <th class="vs-app-table-head">Июл</th>
            <th class="vs-app-table-head">Авг</th>
            <th class="vs-app-table-head">Сен</th>
            <th class="vs-app-table-head">Окт</th>
            <th class="vs-app-table-head">Ноя</th>
            <th class="vs-app-table-head">Дек</th>
          </tr>  
        </thead>
        <tbody>
          <user v-for="(user,i) in users"
                v-bind:months="months" 
                v-bind:year="curYear" 
                v-bind:key="i"
                v-bind:user="user">
          </user>
        </tbody>
      </table>
    </div>  
  </div>
</template>

<script>
  import User from './user';

  export default {
    props:{
      users: Array
    },
    data () {
      return {
        curYear: 2019,
        months: [0,1,2,3,4,5,6,7,8,9,10,11]
      }
    },
    methods: {
      decYear(){
        this.curYear -= 1;
      },

      incYear(){
        this.curYear += 1;
      }
    },
/*     created(){
      debugger;
      let u = this.users;
    },
 */    components:{
      User
    }
  }
</script>

<style lang="scss">

  @mixin controlls {
    display: block;
    width: 18px;
    height: 18px;
    background-position: center;
    background-repeat: no-repeat;
    background-size: contain;
  }

  @mixin flex-align-center {
    display: flex;
    align-items: center;
  }

  .vs-app-table-wrapper {
    width: 100%;
    overflow-x: auto;
  }

  .vs-app-header{
    @include flex-align-center;
    justify-content: space-between;
    background-color: #F7F7F7;
    padding: 15px 15px 10px 15px;
  }

  .vs-app-header__head{
    font-size: 24px;
    font-weight: 300;
    color: #2D2E2E;
    margin: 0;
    text-align: left;
  }

  .vs-app-controlls{
    @include flex-align-center;
  }

  .vs-app-left-controll{
    @include controlls;
    background-image: url('../assets/ic-left.svg');
    margin-right: 15px;
  }

  .vs-app-right-controll{
    @include controlls;
    background-image: url('../assets/ic-right.svg');
    margin-left: 15px;
  }

  .vs-app-cur-year{
    display: block;
    font-size: 18px;
    color: #232323;
  }

  .vs-app-table{
    border-collapse: collapse;
    width: 100%;
  }

  .vs-app-table-head{
    font-size: 10px;
    color: #232323;
    text-align: center;
    background-color: #F7F7F7;
    min-width: 65px;
    padding: 8px 5px;
    border: none;
  }

  .vs-app-table td{
    padding: 8px 5px;
  }
</style>