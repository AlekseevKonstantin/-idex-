<template>
  <div id="app">
    <vacation-schedule v-bind:users="users"></vacation-schedule>

    <transition name="modal">
      <modal v-bind:user="user" 
             v-bind:class="{active: isShow}"
             v-bind:key="isShow"></modal>
    </transition>
  </div>
</template>

<script>

import VacationSchedule from "./components/vacation-schedule";
import Modal from './components/modal';

export default {
  name: 'app',
  data(){
    return {
      users: [
        {
          name: 'Иван',
          surname: 'Иванов',
          photo: 'src/assets/photo-1.png',
          holidays: [
            {
              start: '2019/09/14',
              count: 14
            },

            {
              start: '2019/04/23',
              count: 14
            }
          ],
          limitHolidays: 28
        },
        {
          name: 'Ольга',
          surname: 'Петровна',
          photo: 'src/assets/photo-2.png',
          holidays: [
            {
              start: '2019/10/10',
              count: 14
            },

            {
              start: '2019/03/28',
              count: 14
            }
          ],
          limitHolidays: 28
        }
      ],
      user: {},
      isShow: false
    }
  },
  methods:{
    onMouseOver(e){
      debugger;
      console.log(e);
    }
  },
  mounted(){
    this.$root.$on('emitmouseover', (e) => {
      this.isShow = e.active;
      this.user = e;
    });

    this.$root.$on('emitmouseleave', (e) => {
      this.isShow = e.active;
    })
  },
  components:{
    VacationSchedule,
    Modal
  }
}
</script>

<style lang="scss">
#app {
  position: relative;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2D2E2E;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.modal-enter, .modal-leave-to{
  opacity: 0;
}

.modal-enter-to, .modal-leave{
  opacity: 1;
}

.modal-enter-active, .modal-leave-active{
  transition: opacity .5s ease-in-out;
}

.active{
  display: block !important;
}
</style>
