<template>
    <div>
        <div class="close-information-modal-component" v-on:click="closeModal">&#x2715;</div>
        <div class="information-modal-badge-container">
            <img src ="../assets/logo.png">
        </div>
        <div class="stats-container">
            <div class="information-modal-stat  title">Award for {{title}}</div>
            <div class="information-modal-stat">
                <span>Criteria:</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <span>{{item.award.Criteria}}</span>
            </div>
            <div class="information-modal-stat">
                <span>Evidence:</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <span>{{item.award.Evidence}}</span>
            </div>
            <div class="information-modal-stat">
                <span>Credits:</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <span>{{item.award.Credit}}</span>
            </div>
            <div class="information-modal-stat">Time Spent: &nbsp;&nbsp;&nbsp; {{time}}</div>
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
        document.getElementsByClassName('user-progress-content')[0].style.height = '';
      },
      updateSize(){
        if(document.getElementsByClassName('award-information-modal')){
          let modalHeight = document.getElementsByClassName('award-information-modal')[0].offsetHeight;
          let buttonSize = document.getElementsByClassName('user-progress-navigation')[0].clientHeight;
          let searchSize = document.getElementsByClassName('search-box-container')[0].clientHeight;
          let windowSize = window.innerHeight;

          let maxHeight = windowSize - (buttonSize + searchSize + modalHeight);

          document.getElementsByClassName('user-progress-content')[0].style.height = maxHeight + 'px';
        }
      }
    },
    updated(){
      this.$nextTick(function () {
        this.updateSize();
      })
    },
    mounted(){
      this.updateSize();
    }

  }
</script>

<style>

    .information-modal-badge-container > * {
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto;
        right:0;
        left: 0;

    }

    img{
        max-height: 100%;
    }
    .title{
        font-size: 1.7rem;
    }
    .close-information-modal-component{
        position: absolute;
        right:0;
        background: white;
        width: 20px;
        text-align: center;
        cursor: pointer;
    }
    .information-modal-badge-container{
        min-width: 30%;
        max-width: 30%;
        position: relative;
    }

    .information-modal-stat{
        display: flex;
        width: 100%;
        color: white;
        margin-bottom: 6px;
    }
    .stats-container {
        padding: 16px;
    }
</style>