<template>
    <div>
        <div class="information-container">
            <div class="progress-component-course-title">Completed {{course}}</div>
            <div class="progress-component-time-spent">Time Spent: {{time}}</div>
        </div>

        <div class="progress-component-badge-container"><img src="../assets/logo.png"> </div>
    </div>
</template>

<script>
  export default {
    name:'ProgressComponent',
    props:['item','course'],
    data(){
      return{
        'time': '',
      }
    },
    mounted(){
      let hours = Math.floor(this.item.time_spent/3600);

      let minutes = Math.floor((this.item.time_spent-(3600*hours))/60);

      if(hours < 10 && minutes < 10){
        this.time = '0'+hours+':'+'0'+minutes;
      }
      else if(hours < 10 && minutes > 10){
        this.time = '0'+hours+':'+minutes;
      }
      else if(hours > 10 && minutes < 10){
        this.time = hours+':0'+minutes;
      }
      else {
        this.time = hours+':'+minutes;
  }
    }
  }
</script>

<style>
    .information-container{
        width: 80%;
        padding: 10px;
    }

    .progress-component-course-title{
        float: left;
        width: 80%;
        padding: 8px;
        font-size: 18px;
    }

    .progress-component-time-spent{
        float: left;

        padding: 8px;
        font-size: 14px;
    }

    .progress-component-badge-container{
        float: right;
        min-width: 17%;
        max-width: 17%;
        padding: 12px 16px;
    }
</style>