<template>
    <div>
        <div class="information-container">
            <div class="progress-component-course-title">{{course}}</div>
            <div class="progress-component-time-spent">{{item.time_spent}}</div>
        </div>

        <div class="progress-component-badge-container"><img src="../assets/logo.png"> </div>
    </div>
</template>

<script>
  export default {
    name:'ProgressComponent',
    props:['item','course']
  }
</script>

<style>
    .information-container{
        width: 80%;
    }

    .progress-component-course-title{
        float: left;
        width: 80%;
        padding: 8px;
    }

    .progress-component-time-spent{
        float: left;
        width: 80%;
        padding: 8px;
    }

    .progress-component-badge-container{
        float: right;
        width: 20%;
        padding: 20px;
    }
</style>