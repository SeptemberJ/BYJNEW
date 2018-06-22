<template>
    <div class="Wrap">
	    <div style="width: 100%;position: relative;overflow: hidden;overflow-x: hidden;height: auto;">
	        <div style="background-image: url('static/image/P5/bg.png');width:95%;height: 100%;margin: 0 auto; background-size: cover;">
	            <div class="headBackgroundTwo"></div>
	            <img  style="padding-top: 30px;padding-left: 40%;height: 2%" src="static/image/P5/yulu.png"/>

	      
	            <div style="padding: 10px;margin:10px 10px;text-align: center;background: #ddd">
	                <img @click="toPre" src="image/P5/pre.png" style="height: 2%"/>

	                 <div style="padding:7%;text-align: center;font-size: 1rem">{{selectedData}}</div>

	                <img @click="toNext" src="image/P5/next.png" style="height: 2%"/>
	            </div>

	            <div style="text-align: center;padding-top: 0rem;margin:10px 10px;">
		            <el-input class="upload-text"
		                    type="textarea"
		                      :rows="6"
		                    placeholder="#毕业季，踏上江湖路#写下你最想说的话，生成属于你的江湖语录"
		                    v-model="quotation">
		            </el-input>
		            <el-input class="upload-input"
		                    placeholder="落款姓名"
		                    v-model="name"
		                    clearable  style="margin-top: 10px;">
		            </el-input>
	            </div>

	            <div style="text-align: center;margin-top: 10px;" >
	            	<img :src="imagePath" @click="change" style="padding-bottom: 2rem;height: 4%"/>
	            </div>
	            <div style="position: relative;margin: 0 auto;text-align: center;">
	                <img @click="goBack" src="static/image/P5/4-1.png"/>
	                <img  @click="success" src="static/image/P5/4-2.png" style="margin-left: 20px;" />
	            </div>

	        </div>
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
            name:'',
            quotation:'',
            quote:['为什么毕业要选在夏天？可能这季节眼泪蒸发得比较快。','六月，有人笑着说解脱，有人哭着说不舍','堂堂七尺男儿，扛得住挂科的压力，却扛不住离别的忧伤。','四年时光是最好的下酒菜，吃散伙饭时每个人的酒量都因此变得很好。','同学就是：来时五湖四海，离时天各一方。'],
            num:0,
            selectedData:'为什么毕业要选在夏天？可能这季节眼泪蒸发得比较快。',
            imagePath:'image/P5/know.png',
            check:true
        }
    },
    methods:{
        toPre() {
            if (this.num && this.num > 0) {
                this.num--
                this.selectedData = this.quote[this.num]
                // this.quotation = this.quote[this.num]
            }  else {
                this.selectedData = this.quote[0]
                // this.quotation = this.quote[0]
            }

        },
        toNext() {
            if (this.num < this.quote.length-1) {
                this.num++
                this.selectedData = this.quote[this.num]
                // this.quotation = this.quote[this.num]
            } else {
                this.selectedData = this.quote[this.quote.length-1]
                // this.quotation = this.quote[this.quote.length-1]
            }


        },
        goBack() {
            axios.get(R_PRE_URL + 'serSign?open_id=' + localStorage.getItem("openid")
            ).then((res)=> {
                if(res.data.code == 1){
                	this.$router.push({name:'申请'})
                }else{
                    this.$router.go(-1)
                }
            }).catch((error)=> {
                console.log(error)
            })
        },
        change() {
            this.check = !this.check
            if (this.check) {
                this.imagePath = 'image/P5/know.png'
            } else {
                this.imagePath = 'image/P5/nocheck.png'
            }
        },
        success() {
            var self = this
            if (!this.check) {
                this.$notify({
                    title: '',
                    message: '勾选后才可正常提交',
                    type: 'warning'
                });
                return
            }
            if(this.quotation == '' || this.quotation == 'undefined'){
                this.$notify({
                    title: '',
                    message: '请填写语录！',
                    type: 'warning'
                });
                return
            }
            var DATA = {
                yulu: this.quotation,
                open_id:localStorage.getItem("openid")
            }
            axios.get(R_PRE_URL + 'serSign?open_id=' + localStorage.getItem("openid")
            ).then((res)=> {
                const loadingyulu =this.$loading({
                  lock: true,
                  text: 'Loading',
                  spinner: 'el-icon-loading',
                  background: 'rgba(0, 0, 0, 0.7)',
                  target: document.querySelector('.div1')
                });
                if(res.data.code == 1){
                        axios.post(R_PRE_URL + 'insertSignEntry',DATA
                          ).then((res)=> {
                            if(res.data.code == 0){
                                this.$router.push({
                                path: '/success',
                                //query: {quotation: self.quotation, name: self.name}
                            })
                            }
                          }).catch((error)=> {
                            console.log(error)
                          })
                          loadingyulu.close()
                }else{
                    this.$router.push({
                        path: '/Apply',
                        query: {quotation: self.quotation, name: self.name}
                    })
                    loadingyulu.close()
                }
            }).catch((error)=> {
                console.log(error)
                loadingyulu.close()
            })
        }
    }
  }

</script>
<style lang="scss" scoped>


</style>