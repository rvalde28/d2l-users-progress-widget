<template>
    <div>
        <div class="close-information-modal-component" v-on:click="closeModal">&#x2715;</div>
        <div class="information-modal-badge-container">
            <img src ="../assets/logo.png">
        </div>
        <div class="stats-container">
            <div class="information-modal-stat  title">Award for {{title}}</div>
            <div class="information-modal-stat">Criteria: {{item.award.Criteria}}</div>
            <div class="information-modal-stat">Evidence: {{item.award.Evidence}}</div>
            <div class="information-modal-stat">Credits: {{item.award.Credit}}</div>
            <div class="information-modal-stat">Time Spent: {{time}}</div>
        </div>
    </div>
</template>

<script>
  export default {
    props: ['item','time','title'],
    data(){
      return{

      }
    },
    methods:{
      closeModal(){
        this.$emit('closeModal');
      }
    }

  }
</script>

<style>

    .information-modal-badge-container > * {
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto;
    }

    .title{
        font-size: 1.4rem;
    }
    .close-information-modal-component{
        position: absolute;
        right:0;
        background: white;
        width: 20px;
        text-align: center;
    }
    .information-modal-badge-container{
        min-width: 30%;
        position: relative;
    }

    .information-modal-stat{
        width: 100%;
        color: white;
    }
    .stats-container {
        padding: 16px;
    }
</style>