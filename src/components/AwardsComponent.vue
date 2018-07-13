<template>
    <div>
        <div class="awards-component-badge" v-on:click="triggerModal"><img  class="awards-image" src="../assets/logo.png"></div>
        <div class="awards-criteria" v-on:click="triggerModal"><p>{{item.award.Criteria}}</p></div>
        <div class="award-credit">(Credit: {{item.award.Credit}})</div>
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
        min-width: 17%;
        max-width: 17%;
        padding: 12px 16px;
    }
    img{
        display:block;
        max-width: 100%;
        margin-left: auto;
        margin-right: auto;
        width:auto;
    }

    .awards-criteria{
        width: 70%;
        padding: 12px 16px;
        font-size: 14px;

    }

    p{
        display: table-cell;
        vertical-align: middle;
        height: calc(15vh - 32px);
    }

    .award-credit{
        position: absolute;
        right: 0;
        bottom:0;
        font-style: italic;
        padding-right: 16px;
        font-size: 14px;
    }
</style>
