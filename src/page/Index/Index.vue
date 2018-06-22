<template id="index">
    <div class="Wrap">
        <div class="headBackground"></div>
        <div style="background: url('static/image/P1/1.png') no-repeat 50%;height: 50vh;background-size: 95%"></div>
        <div class="next_item"  @click="gotoApply" style="background: url('static/image/P1/button.png') no-repeat 50%;
        height: 7vh;background-size: 40%;"></div>
        <div class="footBackground" style="background-size: 40%"></div>
        <div style="position: relative;">
            <img style="position:absolute;left: 0;top: 1em;left: 1em;width: 40%;" src="static/image/P1/4.png">
        </div>
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import $ from 'jquery'

  export default{
    data: function () {
        return {
            schoolList:['上海大学','厦门大学']
        }
    },
    mounted: function () {
    	function GetRequest() {
		    return QueryString.data;
		}

		var QueryString = {
	        data: {},
	        Initial: function () {
	            var aPairs, aTmp;
	            var queryString = new String(window.location.search);
	            queryString = queryString.substr(1, queryString.length); //remove   "?"     
	            aPairs = queryString.split("&");
	            for (var i = 0; i < aPairs.length; i++) {
	                aTmp = aPairs[i].split("=");
	                this.data[aTmp[0]] = aTmp[1];
	            }
	        },
	        GetValue: function (key) {
	            return this.data[key];
	        }
	    }
		QueryString.Initial();

		$(document).ready(function() {
		    //$('#open_id').val(GetRequest()["openid"]);
		    console.log(GetRequest()["openid"])
		    var openid = GetRequest()["openid"];
		    localStorage.setItem("openid",openid)

		})
      
    },
    created: function () {
        axios.get(R_PRE_URL + 'serSign?open_id=' + localStorage.getItem("openid")
        ).then((res)=> {
            if(res.data.code == 1){
                    IfSigned = true
                    localStorage.setItem("IfSigned",true)
                    this.$router.push({name:'成功'})
                    
            }
        }).catch((error)=> {
            console.log(error)
        })

    },
    methods: {
        gotoApply() {
        	this.$router.push({name:'申请'})
            
        }
    }
  }

</script>
<style lang="scss" scoped>


</style>
