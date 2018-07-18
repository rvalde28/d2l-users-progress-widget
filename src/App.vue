<template>
  <div id="app">

    <div class="user-progress-navigation">
      <div class="user-navigation-option" id="awards" v-on:click="awardsClick">Awards</div>
      <div class="user-navigation-option" id="progress" v-on:click="progressClick">Progress</div>
    </div>

    <div class="search-box-container"><input type="text" v-model="searchItem" placeholder="Search..."></div>
    <information-modal
            class="award-information-modal"
            v-bind:item="modalItem"
            v-bind:title="modalTitle"
            v-bind:time="modalTime"
            v-on:closeModal="closeModal"
            v-if="isAwards && isModal"></information-modal>

    <div class="user-progress-content">

      <awards-component
              class="awards-component"
              v-if="isAwards && item.award"
              v-for="(item,key) in itemFilter"
              :key="item.id"
              v-bind:item="item"
              v-on:imageClicked="imageClick(key,item)"></awards-component>

      <progress-component
              class="progress-component"
              v-for="(item,key) in itemFilter"
              v-if="isProgress && (item.is_complete === true)"
              :key="item.id"
              v-bind:item="item"
              v-bind:course="key"></progress-component>

      <div class="user-progress-stat-box" v-if="isAwards">
        Total Credit: {{totalPoints}}
      </div>
      <div class="user-progress-stat-box" v-if="isProgress">
        Total time: {{totalTime}}
      </div>
    </div>
  </div>
</template>

<script>
import AwardsComponent from './components/AwardsComponent';
import ProgressComponent from './components/ProgressComponent';
import InformationModal from './components/InformationModalComponent'
import axios from 'axios';

export default {
  name: 'app',
  data(){
    return{
      isAwards: false,
      isProgress: false,
      list: [],
      awardsList: [1,1,1,1,1,1,1],
      progressList: [],
      isModal: false,
      modalItem: '',
      modalTime: '',
      modalTitle: '',
      searchItem: '',
      totalPoints: 0,
      totalTime: 0,
      userId: null,
      axiosInstance: null,
    }
  },
  components: {
    AwardsComponent,
    ProgressComponent,
    InformationModal,
  },
  methods:{
    getContext () {
      let url = null;
      if (this.isDev) {
        url = 'http://smithu.app/api'
      } else {
        url = 'https://udev.smithbuy.com/api'
      }
      this.axiosInstance = axios.create({
        baseURL: url
      })
    },
    getWhoAmI (cb) {
      if (this.isDev) {
        this.userId = 665;
        if (cb) {
          cb()
        }
      } else {
        this.d2lInstance.get('/lp/1.9/users/whoami').then(res => {
          this.userId = res.data.Identifier;
          if (cb) {
            cb()
          }
        }).catch(() => {})
      }
    },
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
      this.isModal = false;
      document.getElementById('awards').classList.remove('active-button');
      document.getElementById('progress').classList.add('active-button');

      if(document.getElementsByClassName('display-awards').length >= 1){
        document.getElementsByClassName('user-progress-content')[0].classList.remove('display-awards');
      }
      document.getElementsByClassName('user-progress-content')[0].style.height = '';

    },
    imageClick(key, item){
      this.isModal = true;

      this.modalItem = item;
      this.modalTitle = key;

      let hours = Math.floor(item.time_spent/3600);

      let minutes = Math.floor((item.time_spent-(3600*hours))/60);

      if(hours < 10 && minutes < 10){
        this.modalTime = '0'+hours+':'+'0'+minutes;
      }
      else if(hours < 10 && minutes > 10){
        this.modalTime = '0'+hours+':'+minutes;
      }
      else {
        this.modalTime = hours+':'+minutes;
      }


    },
    closeModal(){
      this.isModal = false;
    }
  },
  mounted() {

    axios.get('http://localhost:8000/api/progress/967')
      .then(
        response => {
          this.list = response.data;
          Object.keys(this.list).forEach(key => {
            if(this.list[key].award != undefined){
              this.totalPoints += Number(this.list[key].award.Credit);

            }

            if(this.list[key].is_complete === true){
              this.totalTime += Number(this.list[key].time_spent);
            }
          });

          let hours = Math.floor(Number(this.totalTime)/3600);
          let minutes = Math.floor((this.totalTime-(3600*hours))/60);

          if(hours < 10 && minutes < 10){
            this.totalTime = '0'+hours+':'+'0'+minutes;
          }
          else if(hours < 10 && minutes > 10){
            this.totalTime = '0'+hours+':'+minutes;
          }
          else if(hours > 10 && minutes < 10){
            this.totalTime = hours+':0'+minutes;
          }
          else {
            this.totalTime = hours+':'+minutes;
          }


        });

    this.isAwards = true;
    document.getElementById('awards').classList.add('active-button');
    document.getElementsByClassName('user-progress-content')[0].classList.add('display-awards');



  },
  updated(){

  },
  computed:{


   itemFilter(){
     let list = [];
     let returnItem = {

     };

     Object.keys(this.list).forEach(key =>{
       let searchTemp = this.searchItem;

       searchTemp = searchTemp.replace(/\s/g,'').toLowerCase();

       let tempCourse = key;

       tempCourse = tempCourse.replace(/\s/g,'').toLowerCase();

       if(tempCourse.includes(searchTemp)){
         returnItem[key] = this.list[key];
       }
     });

     list.push(returnItem);

     return returnItem;
    }


  }
}
</script>

<style>
  body{
    margin:0;
    cursor: default;
  }

  input{
    width: 100%;
    height: 5vh;
    outline: none;
    border: none;
    padding:0;
    font-size:14px;
  }

  #app {
    font-family: Lato,Lucida Sans Unicode,Lucida Grande,sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .user-progress-navigation{
    display: flex;
    width: 100%;
    background:white;
    height: 6vh;
    top:0;
  }

  .search-box-container{
    height:5vh;
    padding:0 16px;
    box-shadow: 0 2px 4px 0 rgba(0,0,0,.4);
  }

  .user-navigation-option{
    width: 50%;
    padding-top: 10px;
    text-align: center;
    cursor: pointer;
    color: rgb(222, 46, 7);
  }
  .user-navigation-option:hover{
    transition: all .4s ease-in-out;
    background-color: rgb(222, 46, 7);
    color:white;
  }

  .active-button{
    background-color: rgb(222, 46, 7);
    color:white;
  }

  .award-information-modal{
    width:calc(100vw - 32px);
    display: flex;
    background-color: rgb(222, 46, 7);
    color: white;
    box-shadow: 0 2px 4px 0 rgba(0,0,0,.4);
    max-height: 80vh;
    position: relative;
    padding: 16px;
  }

  .user-progress-content{
    width: 100%;
    height: calc(100vh - 11vh);
    overflow-y: auto;
  }

  .progress-component{
    display: flex;
    max-height: 15vh;
  }

  .progress-component:hover{
    box-shadow: 0 0 4px 0 #EE9E2B;
  }

  .user-progress-stat-box{
    position:fixed;
    bottom: 0;
    left:0;
    padding: 8px 20px 8px 20px;
    background-color: rgb(222, 46, 7);
    color: white;
  }
  .awards-component{
    display: flex;
    max-height: 15vh;
    cursor: pointer;
    position:relative;
  }

  .awards-component:hover{
    box-shadow: 0 0 4px 0 rgb(222, 46, 7);
  }

</style>
