<template>
    <div>
        <div class="awards-component-badge" v-on:click="triggerModal"><img  class="awards-image" src="../assets/logo.png"></div>
        <div class="awards-criteria">{{item.award.Criteria}}</div>
    </div>
</template>

<script>
  export default {
    name: 'AwardsComponent',
    props: ['item'],
    methods:{
      triggerModal(){
        this.$emit('imageClicked', this.item)
      }
    }
  }
</script>

<style>
    .awards-component-badge{
        padding:20px;
    }
    img{
        display:block;
        max-width: 100%;
        margin-left: auto;
        margin-right: auto;
        width:auto;

    }


    .awards-criteria{
        padding:20px;
        font-size: 14px;
    }
</style>
