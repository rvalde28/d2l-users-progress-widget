<template>
    <div>
        <div class="information-container">
            <div class="progress-component-course-title">Course</div>
            <div class="progress-component-time-spent">Time Spent</div>
        </div>

        <div class="progress-component-badge-container"> Image</div>
    </div>
</template>

<script>
  export default {

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