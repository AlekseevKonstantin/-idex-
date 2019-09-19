<template>
    <div class="day" 
         v-bind:class="isPastDay + isHoliDay()" 
         v-on:mouseover="emitMouseOver"
         v-on:mouseleave="emitMouseLeave">
    </div>
</template>

<script>
  import Modal from './modal';
  export default {
    props:{
      year: Number,
      month: Number,
      day: Number,
      user: Object
    },
    data(){
      return{
        dateStart: '',
        dateEnd: '',
        count: '',
        caption: ''
      }
    },
    methods:{

      emitMouseOver(e){

        let emitUser = {
          active: true,
          photo: this.user.photo,
          name: this.user.name,
          surname: this.user.surname,
          dateStart: this.dateStart,
          dateEnd: this.dateEnd,
          count: this.count,
          caption: this.caption
        };

        this.$root.$emit('emitmouseover', this.dateStart !== '' ? emitUser: {active: false});
      },
      emitMouseLeave(){
        let emitUser = {active: false};

        this.$root.$emit('emitmouseleave', emitUser);
      },
      isHoliDay(){
        let now = new Date(),
            date = new Date(this.year, this.month, this.day);
        
        for(let i = 0, len = this.user.holidays.length; i < len; i += 1){
          let holidayInit = new Date(Date.parse(this.user.holidays[i].start)),
              holiday = holidayInit;

          for(let j = 0, count = this.user.holidays[i].count; j <= count; j += 1){
            
            if(+holiday.valueOf() == +date.valueOf() && +date.valueOf() < +now.valueOf()){
              this.dateStart = +holidayInit.valueOf();
              this.dateEnd = holidayInit.setDate(holidayInit.getDate()+this.user.holidays[i].count);
              this.isHoliDay = true;
              this.count = this.user.holidays[i].count;
              this.caption = 'отпуск истек'
              return ' past-holiday '
            }else if(+holiday.valueOf() == +date.valueOf() && +date.valueOf() >= +now.valueOf()){
              this.dateStart = +holidayInit.valueOf();
              this.dateEnd = holidayInit.setDate(holidayInit.getDate()+this.user.holidays[i].count);
              this.isHoliDay = true;
              this.count = this.user.holidays[i].count;
              this.caption = 'отпуск';
              return ' holiday '
            }

            holiday.setDate(holiday.getDate() + 1);
          }
        }

        return '';
      }
    },
    computed:{
      isPastDay(){
        let now = new Date(),
            date = new Date(this.year, this.month, this.day);
        
        now.setDate(now.getDate()-1);

        return +date.valueOf() < +now.valueOf() ? ' past-days ': '';
      },

      
    },
    components:{
      Modal
    }
  }
</script>

<style lang="scss">

  .day{
    width: 8px;
    height: 3px;
    margin: 0;
    padding: 0;
    background-color:#EAF9FF;
  }

  .day.holiday{
    background-color: #1EBEB4;
  }

  .day.past-holiday{
    background-color: #F16953;
  }

  .past-days{
    background-color: #F6F6F6;
  }
</style>