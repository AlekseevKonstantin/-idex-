<template>
  <div class="vs-app-modal">
    <div class="vs-app-modal-row">
      <div class="img-wrapper">
        <img v-bind:src="user.photo" alt="" class="vs-app-modal-img"/>
      </div>
      <p class="vs-app-modal-user">
        <span class="vs-app-modal-user-name">{{user.name}}</span>
        <span class="vs-app-modal-user-surname">{{user.surname}}</span>
      </p>
    </div>
    <div class="vs-app-modal-row" style="margin-top: 25px;">
      <span class="vs-app-modal-color-indicator" v-bind:class="user.caption === 'отпуск истек'? ' red ': ' green '"></span>
      <p class="vs-app-modal-date-wrapper">
        <span class="vs-app-modal-date">
          <span class="vs-app-modal-date-start">{{dateStart}}</span>
          <span>-</span>
          <span class="vs-app-modal-date-start">{{dateEnd}}</span>
          <span>({{user.count}})</span>
        </span>
        <span class="vs-app-modal-date-caption">{{user.caption}}</span>
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      user: Object
    },
    computed:{
      dateStart(){
        let date = new Date(this.user.dateStart),
            day = date.getDate() < 10 ? '0' + date.getDate():date.getDate(),
            month = date.getMonth() < 10 ? '0' + date.getMonth(): date.getMonth();
        return day+'.'+month+'.'+date.getFullYear();
      },
      dateEnd(){
        let date = new Date(this.user.dateEnd),
            day = date.getDate() < 10 ? '0' + date.getDate():date.getDate(),
            month = date.getMonth() < 10 ? '0' + date.getMonth(): date.getMonth();
        return day+'.'+month+'.'+date.getFullYear();
      }
    } 
  }
</script>

<style lang="scss">
  @mixin do-flex{
    display: flex;
  }

  .vs-app-modal-row{
    @include do-flex;
    align-items: flex-start;
  }

  .vs-app-modal-img{
    display: block;
    width: 54px;
    height: auto;
  }

  .vs-app-modal {
    position: absolute;
    top: 120%;
    left: 45%;
    z-index: 300;
    background: #FFFFFF;
    box-shadow: 0 0 4px 0 rgba(107,107,107,0.50);
    border-radius: 4px;
    border-radius: 4px;
    padding: 15px;
    display: none; 
  }

  .vs-app-modal-user{
    @include do-flex;
    flex-direction: column;
    align-items: flex-start;
    min-width: 300px;
    max-width: 345px;
    width: 100%;
    margin: 0 0 0 20px;
    font-size: 14px;
    color: #000000;
    font-weight: 700;
  }

  .vs-app-modal-date-wrapper{
    @include do-flex;
    flex-direction: column;
    align-items: flex-start;
    margin: 0 0 0 10px;
  }

  .vs-app-modal-color-indicator{
    display: inline-block;
    width: 12px;
    height: 16px;
  }

  .vs-app-modal-date-caption{
    color: #AEAEAE;
  }

  .red{
    background-color: #F16953 !important;
  }

  .green{
    background-color: #1EBEB4 !important;
  }
</style>