<template>
  <div id="app">

    <div class="user-progress-navigation">
      <div class="user-navigation-option" id="awards" v-on:click="awardsClick">Awards</div>
      <div class="user-navigation-option" id="progress" v-on:click="progressClick">Progress</div>
    </div>

    <div class="user-progress-content">
      <awards-component
              class="awards-component"
              v-if="isAwards"
              v-for="item in list"
              :key="item.id"
              v-bind:item="item"></awards-component>

      <progress-component
              class="progress-component"
              v-if="isProgress"
              v-for="item in list"
              :key="item.id"
              v-bind:item="item"></progress-component>

      <div class="user-progress-stat-box">
        Total Points:
      </div>
    </div>


  </div>
</template>

<script>
import AwardsComponent from './components/AwardsComponent';
import ProgressComponent from './components/ProgressComponent';

export default {
  name: 'app',
  data(){
    return{
      isAwards: false,
      isProgress: false,
      list: [1,2,3,4]
    }
  },
  components: {
    AwardsComponent,
    ProgressComponent
  },
  methods:{
    awardsClick(){
      this.isAwards = true;
      this.isProgress = false;

      document.getElementsByClassName('user-progress-content')[0].classList.add('display-awards');

      document.getElementById('awards').classList.add('active-button');
      document.getElementById('progress').classList.remove('active-button');
    },
    progressClick(){
      this.isProgress = true;
      this.isAwards = false;
      document.getElementById('awards').classList.remove('active-button');
      document.getElementById('progress').classList.add('active-button');

      if(document.getElementsByClassName('display-awards').length >= 1){
        document.getElementsByClassName('user-progress-content')[0].classList.remove('display-awards');
      }
    },

  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  .user-progress-navigation{
    display: flex;
  }

  .user-navigation-option{
    width: 50%;
    padding: 10px;

  }
  .user-navigation-option:hover{
    transition: all .4s ease-in-out;
    background-color: #2B57EE;
    color:white;
  }

  .active-button{
    background-color: #2B57EE;
    color:white;
  }


  .display-awards{
    display: grid;
    grid-template-columns: 33.33% 33.33% 33.33%;
  }



  .user-progress-content{
    width: 100%;

  }


  .progress-component{
    display: flex;
    border: 1px solid black;
  }

  .user-progress-stat-box{
    position:absolute;
    bottom: 0;
    left:0;
    padding: 20px;
  }
  .awards-component{


  }



</style>
