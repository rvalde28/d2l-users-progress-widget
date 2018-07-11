<template>
    <div>
        <div class="close-information-modal-component"></div>
        <div class="information-modal-badge-container">
            <img src ="../assets/images.jpg">
        </div>

        <div class="information-modal-stat">{{item.award.Credit}}</div>
        <div class="information-modal-stat">{{item.award.Criteria}}</div>
        <div class="information-modal-stat">{{item.award.Evidence}}</div>
        <div class="information-modal-stat">{{time}}</div>
    </div>
</template>

<script>
  export default {
    props: ['item'],
    data(){
      return{
        time:''
      }
    },
    mounted(){
      let hours = Math.floor(this.item.time_spent/3600);
      console.log(hours);
      let minutes = Math.floor((this.item.time_spent-(3600*hours))/60);
      console.log(minutes);

      if(hours.length === 1 && minutes.length === 1){
        let time = '0'+hours+':'+'0'+minutes;

        this.time = time;
      }

    }
  }
</script>

<style>

</style>