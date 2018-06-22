<template id="success">
    <div class="Wrap">
        <div class="headBackground"></div>
        <div style="position: relative;width: 90%;height:250px;left: 5%;top: 1em;border: 0px solid red;">
            <img style="width: 100%;position:absolute;height: 100%;" src="static/image/P3/successCommit.png" >
            <img style="width: 40%;position: absolute;left: 30%;bottom:0px;height: 2rem" src="static/image/P3/2.png" @click="gotoApply">
        </div>
        <div class="footBackground" style="background-size: 35%;padding-top: 95%"></div>
        <div style="position: relative;">
                <img style="position:absolute;left: 0;top: -250px;left: 1em;width: 40%;" src="static/image/P1/4.png">
            </div>
    </div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
import Qs from 'qs'

  export default{
  	data: function () {
        return {
        }
    },
    methods:{
        gotoApply() {
            this.$router.push({name:'语录'})
        }
    }

  }
</script>