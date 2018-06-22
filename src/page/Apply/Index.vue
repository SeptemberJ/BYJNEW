<template>
    <div class="Wrap">
    <!-- <div class="background" style="width: 160%;height: 155%;overflow:hidden"> -->
    <!-- <div class="background" style="">
        <div class="headBackground"></div>
    <div> -->
    <div class="headBackground"></div>
    <el-form :model="form" ref="form" :rules="rules" class="demo-ruleForm" label-width="120" label-position="left" style="margin-top: 10px">
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="省份" required>
                    <el-row :gutter="19" type="flex" class="row-bg" justify="start">
                        <!-- <el-col :span="2">
                            <span style="color: #fff;">省份</span>
                        </el-col> -->
                        <el-col :span="8">
                            <el-form-item prop="province" style="">
                                <el-select v-model="form.province" placeholder="" style="" @change="onChangeProvince">
                                    <el-option v-for="(ProvinceItem,ProvinceIdx) in ProvinceList" :label="ProvinceItem.pr_province" :value="ProvinceItem.pr_province"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                        <el-col :span="2">
                            <span style="color: #fff; font-size: 1rem;">市</span>
                        </el-col>
                        <el-col :span="8">
                            <el-form-item prop="city" style="float: right;">
                                <el-select v-model="form.city" placeholder="" style="" @change="onChangeCity">
                                    <el-option v-for="(CityItem,CityIdx) in CityList" :label="CityItem.ci_city" :value="CityItem.ci_city"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="学校"  prop="school" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-select v-model="form.school" placeholder="请选择学校" @change="onChangeSchool">
                                <el-option v-for="(School,SchoolIdx) in SchoolList" :label="School.sh_shool" :value="School.sh_shool"></el-option>
                            </el-select>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="学院" prop="college" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input v-model="form.college"></el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="专业" prop="profession" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input v-model="form.profession"></el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="班级" prop="class" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input v-model="form.class"></el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="申领人姓名" prop="name" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input v-model="form.name"></el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="联系人电话" prop="mobile" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input v-model="form.mobile"></el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="收货地址" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="end">
                        <el-col :span="8" style="padding:0 5px;">
                            <el-form-item prop="addressProvince">
                                <el-select v-model="form.address.province" placeholder="" style="width: 100%" @change="onChangeAdProvince">
                                    <el-option v-for="(Ad_ProvinceItem,Ad_ProvinceIdx) in AddressProvinceList" :label="Ad_ProvinceItem.areaname" :value="Ad_ProvinceItem.areaname"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                        <el-col :span="8" style="padding:0 5px;">
                            <el-form-item prop="addressCity" style="width: 100%">
                                <el-select v-model="form.address.city" placeholder="" style="width: 100%"  @change="onChangeAdCity">
                                    <el-option v-for="(Ad_CityItem,Ad_CityIdx) in AddressCityList" :label="Ad_CityItem.areaname" :value="Ad_CityItem.areaname"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                        <el-col :span="8" style="padding:0 5px;">
                            <el-form-item prop="addressArea">
                                <el-select v-model="form.address.area" placeholder="" style="width: 100%"  @change="onChangeAdArea">
                                    <el-option v-for="(Ad_AreaItem,Ad_AreaIdx) in AddressAreaList" :label="Ad_AreaItem.areaname" :value="Ad_AreaItem.areaname"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20" type="flex" class="row-bg" justify="end">
            <el-col :span="18" style="padding:0">
                <el-form-item prop='addressName' >
                    <el-input v-model="form.address.name"></el-input>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item prop="identity" label="证件信息">
                    <el-row :gutter="20" type="flex" class="row-bg" justify="end">
                        <el-col :span="12" style="background-color: white;overflow: hidden;">
                            <div style="text-align: center;" >
                            
							<el-upload style="height:100px;position:relative;"
							 class="avatar-uploader"
							action=""
							:before-upload="Reject"
							:on-change="changeFile"
							>	
							  <div style="width:100%;height:100px;position:absolute;top:0;left:0">
								  
								  <span style="color:#000;display:block;line-height:0px;padding-top:25px;"><i class="el-icon-picture"></i><p style="margin-top:20px;">上传学生证</p></span>
							  </div>
							</el-upload>
                            </div>
                        </el-col>
                        <el-col :span="12" style="background-image: url('static/image/p2/1.png');position:relative;">
                            
                                <div id="identityPic"  ></div>
                                <div id='identityPicTip' @click="openImage" style="
                                text-align: center;color: white;position:relative;z-index: 99;">查看证件范例支持JPG/PNG格式文件</div>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
        <el-row :gutter="20">
            <el-col :span="24">
                <el-form-item label="江湖语录" prop="quotation" required>
                    <el-row :gutter="20" type="flex" class="row-bg" justify="start">
                        <el-col :span="18">
                            <el-input id="goToUpload" @focus="goToUpload"
                                    type="textarea"
                                    placeholder="" :rows="3"
                                    v-model="form.quotation">
                            </el-input>
                        </el-col>
                    </el-row>
                </el-form-item>
            </el-col>
        </el-row>
    </el-form>
    <div style="position: relative;">
        <img @click="submitForm('form')" style="position:absolute;right: 20%; width: 40%" src="static/image/P2/submit.png">
        <div  @click="submitForm('form')" style="position:absolute;right: 20%; width: 40%;z-index: 99999; height: 100px;background: transparent; overflow: hidden;" ></div>
        <img style="position:absolute;left: 0;top: 0;left: 10px;width: 30%;" src="static/image/P1/4.png">
    </div>


       </div>

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
      	dialogImageUrl: '',
        dialogVisible: false,
      	fileList2: [{name: 'food.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}, {name: 'food2.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}],
      	ProvinceList:[],
            CityList:[],
            CityId:'',
            SchoolList:[],
            AddressProvinceList:[],
            AddressCityList:[],
            AddressAreaList:[],
            form: {
                province:'',
                city:'',
                school:'',
                college:'',
                profession:'',
                class:'',
                name:'',
                mobile:'',
                address:{
                    province:'',
                    city:'',
                    area:'',
                    add:''
                },
                identity:'',
                quotation:'',
                identityPic:''
            },
            rules:{
                province: [
                    { required: true, message: '请选择省份', trigger: 'change' },
                    // {validator: validateProvince, trigger: 'change'}
                ],
                city: [
                    { required: true, message: '请选择城市', trigger: 'change' }
                ],
                school: [
                    { required: true, message: '请选择学校', trigger: 'change' },
                ],
                college: [
                    { required: true, message: '请输入学院', trigger: 'blur' },
                ],
                profession: [
                    { required: true, message: '请输入专业', trigger: 'blur' },
                ],
                class: [
                    { required: true, message: '请选择班级', trigger: 'change' },
                ],
                name: [
                    { required: true, message: '请输入申领人姓名', trigger: 'blur' },
                    // { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
                ],
                mobile: [
                    { required: true, message: '请输入联系人电话', trigger: 'blur' },
                    // { type: 'mphone', message: '请输入正确的联系人电话', trigger: ['blur', 'change'] }
                ],
                // addressProvince: [
                //     {required: true, message: '请选择收货省地址', trigger: 'change'},
                // ],
                // addressCity: [
                //     {required: true, message: '请选择收货市地址', trigger: 'change'},
                // ],
                // addressArea: [
                //     {required: true, message: '请选择收货区地址', trigger: 'change'},
                // ],
                // addressName: [
                //     {required: true, message: '请选择收货详细地址', trigger: 'blur'},
                // ],
                identity: [
                    {required: true, message: '请上传证件信息', trigger: 'blur'},
                ],
                quotation: [
                    {required: true, message: '请上传你的江湖语录', trigger: 'blur'},
                ]
            },
      	form2: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
        
      }
    },
    mounted:function () {
        var self = this
        this.$nextTick(function () {
            // Code that will run only after the
            // entire view has been rendered
            // document.getElementById("goToUpload").onblur(function () {
            //     console.log('sssss')
            // })

            if (this.$route.query && this.$route.query.quotation) {
                self.form.quotation = this.$route.query.quotation
            }
        })
        if(JSON.parse(localStorage.getItem("dataInfo")).identityPic){
            document.getElementById("identityPicTip").style.display = 'none'
        }
        
        document.getElementById("identityPic").style.backgroundImage = 'url('+JSON.parse(localStorage.getItem("dataInfo")).identityPic+')'
    },
   created() {
   	if(localStorage.getItem("dataInfo")){
            console.log(JSON.parse(localStorage.getItem("dataInfo")))
            this.form = JSON.parse(localStorage.getItem("dataInfo"))

        }
        
        axios.get(R_PRE_URL + 'provinceList'
        ).then((res)=> {
            this.ProvinceList = res.data.provinceList
        }).catch((error)=> {
        console.log(error)
        })
   	this.GetAddressProvinceList()
     
   },
   computed: {
    
   },
    components: {
      
    },
    
    methods: {
    	handleRemove(file, fileList) {
	        console.log(file, fileList);
	    },
	    Reject(){

	    },
	    handlePictureCardPreview(file) {
	      	alert('hahah')
	        this.dialogImageUrl = file.url;
	        this.dialogVisible = true;
	    },
    	onSubmit() {
        	console.log('submit!');
      	},
       submitForm(formName) {
            
            var self = this
            let isSuccess = true
            var DATA = {
                fprovince:this.form.province,
                fcity:this.form.city,
                fschool:this.form.school,
                xueyuan:this.form.college,
                fprofessional:this.form.profession,
                fclass:this.form.class, //--------
                fname:this.form.name,
                fmobile:this.form.mobile,
                sh_province:this.form.address.province,
                sh_city:this.form.address.city,
                sh_area:this.form.address.area,
                sh_address:this.form.address.name,
                fpic:this.form.identity,
                yulu:this.form.quotation,
                open_id:localStorage.getItem("openid")
            };
            console.log(DATA)
            this.$refs.form.validate((valid) => {
                if(!valid){
                    isSuccess = false;
                    return false;
                }
            });
            if (!isSuccess) {
                return
            }
            
            axios.post(R_PRE_URL + 'insertSign',DATA
              ).then((res)=> {
                const loadingSubmit =this.$loading({
                  lock: true,
                  text: 'Loading',
                  spinner: 'el-icon-loading',
                  background: 'rgba(0, 0, 0, 0.7)',
                  target: document.querySelector('.div1')
                });
                if(res.data.code == 0){
                    this.$router.push({name:'成功'})
                    loadingSubmit.close()
                }
              }).catch((error)=> {
                console.log(error)
                loadingSubmit.close()
              })


        //     this.$router.push({
        //         path: '/success'
        // //         // query: {activity: JSON.stringify(this.pageData[index])}
        //     })
        },
        updateCity(){
            var that = this
            this.ProvinceList.map(function(item,idx){
                if(item.pr_province == that.form.province){
                    that.GetCityList(item.pr_id)
                }
            })
        },
        updateSchool(){
            var that = this
            this.CityList.map(function(item,idx){
                if(item.ci_city == that.form.city){
                    that.GetSchoolList(item.ci_id)
                }
            })
        },
        GetCityList(ProvinceId){
            axios.get(R_PRE_URL + 'cityList?provinceid=' + ProvinceId
            ).then((res)=> {
                this.CityList = res.data.cityList
            }).catch((error)=> {
                console.log(error)
            })
        },
        GetSchoolList(CityId){
            axios.get(R_PRE_URL + 'schoolList?cityid=' + CityId
            ).then((res)=> {
                this.SchoolList = res.data.schoolList
            }).catch((error)=> {
                console.log(error)
            })
        },
        GetAddressProvinceList(){
            axios.get(R_PRE_URL + 'ssqList?ssqid=' + 0
            ).then((res)=> {
                this.AddressProvinceList = res.data.ssqList
            }).catch((error)=> {
                console.log(error)
            })
        },
        GetAddressCityList(ProvinceId){
            axios.get(R_PRE_URL + 'ssqList?ssqid=' + ProvinceId
            ).then((res)=> {
                this.AddressCityList = res.data.ssqList
            }).catch((error)=> {
                console.log(error)
            })
        },
        GetAddressAreaList(CityId){
            axios.get(R_PRE_URL + 'ssqList?ssqid=' + CityId
            ).then((res)=> {
                this.AddressAreaList = res.data.ssqList
            }).catch((error)=> {
                console.log(error)
            })
        },
        //
        onChangeProvince(){
            this.form.city = ''
            this.form.school = ''
            this.updateCity()

        },
        onChangeCity(){
            this.form.school = ''
            this.updateSchool()
        },
        onChangeSchool(e){
            console.log(e)
        },
        onChangeAdProvince(e){
            var that = this
            this.AddressProvinceList.map(function(item,idx){
                if(item.areaname == e){
                    that.GetAddressCityList(item.id)
                }
            })
            this.form.address.city = ''
            this.form.address.area = ''
             // sh_province:this.form.address.province,
             //    sh_city:this.form.address.city,
             //    sh_area:this.form.address.area,
        },
        onChangeAdCity(e){
            var that = this
            this.AddressCityList.map(function(item,idx){
                if(item.areaname == e){
                    that.GetAddressAreaList(item.id)
                }
            })
            this.form.address.area = ''
        },
        onChangeAdArea(e){
            
        },
        changeFile(file, fileList) {
        	console.log('file===')
        	console.log(file)
		    var That = this
		    
		    //this.imageUrl = URL.createObjectURL(file.raw);
		    var reader = new FileReader();
		    reader.readAsDataURL(file.raw);
		    reader.onload = function(e){ 
		         // this.result这个就是base64编码了
		        That.form.identityPic = this.result
	            document.getElementById("identityPic").style.backgroundImage = 'url('+this.result+')'
	            document.getElementById("identityPicTip").style.display = 'none'
	         }
	        var FileData = {
                imgStr:That.form.identityPic.replace(/^data:image\/(jpeg|png|gif|jpeg);base64,/,'')
             }
	         axios.post(R_PRE_URL + 'uploadBase64',Qs.stringify(FileData)
                ).then((res)=> {
                    if(res.data.code == 0){
                        That.form.identity = res.data.fileName
                        loadingItem.close();
                    }
                }).catch((error)=> {
                    console.log(error)
                    //loadingItem.close();
                })
	           
		   
		 },

        onRead2(File) {
        	console.log('File---')
        	console.log(File)
            //this.form.identity = File.file.name
            const loadingItem =this.$loading({
              lock: true,
              text: 'Loading',
              spinner: 'el-icon-loading',
              background: 'rgba(0, 0, 0, 0.7)',
              target: document.querySelector('.div1')
            });

            var that2 = this
            var FileData = File.content
            this.form.identityPic = File.content
            document.getElementById("identityPic").style.backgroundImage = 'url('+File.content+')'
            document.getElementById("identityPicTip").style.display = 'none'

            var file = File.file
            var reader = new FileReader()
            reader.readAsDataURL(file)
            reader.onload = function() {
              img.src = this.result
            }

            var img = new Image,
              width = 1024, //image resize   压缩后的宽
              quality = 0.8, //image quality  压缩质量
              canvas = document.createElement("canvas"),
              drawer = canvas.getContext("2d");
            img.onload = function() {
              canvas.width = 500;
              canvas.height = 500;;
              drawer.drawImage(img, 0, 0, canvas.width, canvas.height);
              //上传到七牛云
              var base64 = canvas.toDataURL("image/jpeg", quality); // 这里就拿到了压缩后的base64图片
              var FileData = {
                imgStr:base64.replace(/^data:image\/(jpeg|png|gif|jpeg);base64,/,'')
                }

                axios.post(R_PRE_URL + 'uploadBase64',Qs.stringify(FileData)
                ).then((res)=> {
                    if(res.data.code == 0){
                        that2.form.identity = res.data.fileName
                       
                        loadingItem.close();
                    }
                }).catch((error)=> {
                    console.log(error)
                    loadingItem.close();
                })
              }

            
        },
        OnErrorPic(){
            // this.$alert('图片太大');
        },
        goToUpload() {
            localStorage.setItem('dataInfo',JSON.stringify(this.form))
            this.$router.push({name:'语录'})
            
        },
        resetForm(formName) {
            this.$refs[formName].resetFields();
        },
        openImage() {
            this.$alert('<img src="https://wxmms.swissems.cn/byj/example.jpg" style="width:100%"/>', '学生证图片范例', {
                dangerouslyUseHTMLString: true
            });
        }
      
    }
  }

</script>
<style lang="scss" scoped>
.el-form--label-left{
	color:#fff !important;
}
 .el-form-item__label{
	color:#fff !important;
}



</style>
