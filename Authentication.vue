<!--页面css样式-->
<style scoped lang='scss'>
    .resg{
        /*background: #f2f6f7;*/
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
        // float:left;
        box-sizing: border-box;
    }
    .titleClass{
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
        background: #fff;
    }
    .cation {
        padding-top: $top;
        // overflow-x: hidden;
        box-sizing: border-box;
    }
    .cation ::-webkit-input-placeholder {
        /* WebKit browsers */
        font-size: .45rem
    }

    .cation :-moz-placeholder {
        /* Mozilla Firefox 4 to 18 */
        font-size: .45rem
    }

    .cation ::-moz-placeholder {
        /* Mozilla Firefox 19+ */
        font-size: .45rem
    }

    .cation :-ms-input-placeholder {
        /* Internet Explorer 10+ */
        font-size: .45rem
    }

    .cation h5{
        color: #1e1e1e;
        width: 100%;
        text-align: center;
        font-size: 0.48rem;
        padding-top: 0.4rem;
    }
    .member h6{
        font-size: 0.5rem;
        padding: 0.38rem;
    }
    .in_list{
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }
    .in_list li{
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden ;
        margin-left: 0.4rem;
    }
    .in_list li a{
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        line-height: 1.3rem;
        min-height: 1.49rem;
    }
    .in_list li a label{
        font-size: 0.48rem;
        color: #1e1e1e;
    }
    .in_list .message{
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.4rem;
        line-height: 1.44rem;
        display: inline-block;

    }
    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        font-family: "微软雅黑";
         text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }
    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background: url(../assets/img/img_14.png)no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }
    .in_list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }
    .foot{
        color: #828282;
        font-size: 0.38rem;
        padding: 0 0.4rem 0.7rem;
    }
    .nav{
        width: 50%;
        height: 1rem;
        border:1px solid #377bee;
        border-radius: 5px;
        margin: 0.5rem auto;
    }
    .nav ul{
        width: 100%;
    }
    .nav ul li{
        border-right: 1px solid #377bee;
        font-size: 0.4rem;
        color: #377bee;
        width: 50%;
        float: left;
        height: 0.97rem;
        line-height: 0.97rem;
        text-align: center;
    }
    .nav ul li:last-child{
        border-right:none;
    }
    .nav ul li.cur{
        background: #377bee;
        color: #fff;
    }
    .sub_btn2{
        padding:0.63rem 0.4rem 1.3rem;
    }
    .prompt{
        background: #f0f4fa;
        color: #787878;
        font-size: .3rem;
        padding:0 .38rem;
        line-height: .6rem;
        padding-bottom: .5rem;
        box-sizing: border-box;
    }
    .per-info{
        background: #f0f4fa; 
    }
    .denity{
        width: 100%;
        background: white;
        box-sizing: border-box;
        padding-bottom:.7rem; 
        ul{
            display: flex;
            justify-content: space-between;
            padding: 0 .38rem;
            li{
                background: #f0f4fa;
                position: relative;
                    margin-right: .38rem;
                input{
                    position: absolute;
                    font-size: .001rem;
                    width: 100%;
                    height: 100%;
                    top:0;
                    left: 0;
                    opacity: 0;
                }
                img{
                    width: 4.8rem;
                    height: 3.7rem;
                }
            }
        }
    }
    .personalWithCard{
        padding: 0 .38rem;
        position: relative;
        input{
            position: absolute;
            font-size: .001rem;
            width: 90%;
            height: 100%;
            top:0;
            left: .38rem;
            opacity: 0;
        }
        img{
            width: 10.1rem;
            height: 4.5rem;
        }
    }
    .info-title{
        font-weight: normal;
    }
</style>
<template>
    <!--会员认证-->
    <div class="cation">
        <h5 >填写<span v-if="$route.query.current">企业</span>认证信息</h5>
        <div class="nav" v-if="!$route.query.current">
            <ul>
                <li :class="{'cur':current}" @click="change()">个人认证</li>
                <li :class="{'cur':!current}" @click="change()">企业认证</li>
            </ul>
        </div>
        <!-- 企业 -->
        <div class="enterprise" v-if="!current">
            <div class="member">
                <h6>企业资料</h6>
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>企业名称</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.en_name" type="text" class="text" placeholder="请输入" >
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>注册资金</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.en_regmoney" type="number" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>法人姓名</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.en_person_name" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.en_person_idcard" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.en_contact" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="member">
                <h6  class="per-info">负责人资料</h6>
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>负责人</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.enuser_name" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.enuser_idcard" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.enuser_contact" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <!-- <li>
                            <a>
                                <label>工作地址</label>
                                <span class="arrow_right"></span>
                                <span class="message">
                                    <input v-model="form.enuser_address" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li> -->
                        <li class="sizePosition">
                            <a >
                                <label >工作地址</label>
                                <el-cascader
                                    :options="options2"
                                    @active-item-change="handleItemChange"
                                    :props="props"
                                    @change = "getSelectedCity"
                                >
                                </el-cascader>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>

            <!-- 上传图片资料 -->
            <div class="member">
                <h6  class="per-info">企业信息录入</h6>
                <div  class="prompt">请上传认证所需要资料，以便顺利通过审核，上传信息及照片仅供平台审核使用，请放心上传</div>
                <div class="denity clearfix">
                    <h6 class="titleClass info-title" >
                            营业执照
                    </h6>
                    <div class="personalWithCard" @click="uplaodFile5">
                        <img :src="host+form.license_card" v-if="form.license_card">
                        <img src="../assets/img/license.png" v-else>
                        <!-- <input type="file" @change="uplaodFile5" class="license_file"> -->
                    </div>
                    <h6 class="titleClass info-title" >
                        法人身份证
                    </h6>
                    <ul>
                        <li class="cardUpPosition" @click="uplaodFile1">
                            <img :src="host+form.legal_idcard_up" v-if="form.legal_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input type="file" @change="uplaodFile1" class="legal_file_up"> -->
                        </li>
                        <li class="cardDownPosition" @click="uplaodFile2">
                            <img :src="host+form.legal_idcard_down" v-if="form.legal_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input type="file" @change="uplaodFile2" class="legal_file_down"> -->
                        </li>
                    </ul>
                    <h6 class="titleClass info-title" >
                        负责人身份证
                    </h6>
                    <ul>
                        
                        <li class="cardUpPosition" @click="uplaodFile3">
                            <img :src="host+form.duty_idcard_up" v-if="form.duty_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input type="file" @change="uplaodFile3" class="duty_file_up"> -->
                        </li>
                        <li class="cardDownPosition" @click="uplaodFile4">
                            <img :src="host+form.duty_idcard_down" v-if="form.duty_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input type="file" @change="uplaodFile4" class="duty_file_down"> -->
                        </li>
                    </ul>
                </div>
            </div>

            <div class="sub_btn">
                <a  @click="postData">提交信息</a>
            </div>
            
        </div>
        <!-- 个人 -->
        <div class="personal" v-if="current">
            <div class="member">
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>姓名</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="user.per_name" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="user.per_idcard" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系电话</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="user.per_iphone" type="text" class="text" placeholder="请输入">
                                </span>
                            </a>
                        </li>
                        <li class="sizePosition">
                            <a >
                                <label>工作地址</label>
                                <el-cascader
                                    :options="options2"
                                    @active-item-change="handleItemChange"
                                    :props="props"
                                    @change = "getSelectedCity"
                                >
                                </el-cascader>
                            </a>

                        </li>
                    </ul>
                </div>
            </div>
            <div class="member">
                <h6 class="per-info">个人信息录入</h6>
                <p class="prompt">请上传认证资料，以便顺利通过审核，上传信息及照片仅供平台审核使用，请放心上传</p>
                <div class="titleClass" >
                    请上传认证人身份证正反面照片。
                </div>
                <div class="denity clearfix">
                    <ul>
                        <li class="personal_up" @click="uplaodUp">
                            <img  :src="host+user.per_idcard_up" v-if="user.per_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input type="file" @change="uplaodUp" class="file_up"> -->
                        </li>
                        <li class="personal_down" @click="uplaodDown">
                            <img :src="host+user.per_idcard_down" v-if="user.per_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input type="file" @change="uplaodDown" class="file_down"> -->
                        </li>
                    </ul>
                    <div class="resg ">
                        请上传您的半身手持身份证照。
                    </div>
                    <div class="personalWithCard clearfix" @click="uplaodPersonalCard">
                        <img :src="host+user.personal_with_card" v-if="user.personal_with_card">
                        <img src="../assets/img/self_card.png" v-else>
                        <!-- <input type="file" @change="uplaodPersonalCard"> -->
                    </div>
                </div>
                <div class="sub_btn sub_btn2">
                    <a @click="userPostData">提交信息</a>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                form:{
                    en_name:'',
                    en_regmoney:'',
                    en_person_name:'',
                    en_person_idcard:'',
                    en_contact:'',
                    enuser_name:'',
                    enuser_idcard:'',
                    enuser_contact:'',
                    legal_idcard_up:'',
                    legal_idcard_down:'',
                    duty_idcard_up:'',
                    duty_idcard_down:'',
                    license_card:'',
                    enuser_address:'',
                    city_id : '',
                },
                user:{
                    per_name:'',
                    per_idcard:'',
                    per_iphone:'',
                    per_idcard_up:'',
                    per_idcard_down:'',
                    personal_with_card:'',
                    per_address:'',
                    city_id : '',
                },
                current:true,
                host:units.getHost(),
                provinces:{},
                provinceId:'',
                provinceName:'',
                cityDatas:{},
                imgtype:'',
                //级联选择器组件 by jfeng
                options2: [],
                props: {
                    value: 'label',
                    children: 'cities'
                },
            }
        },
        methods: {
            handleItemChange(val) {
                setTimeout(_ => {
                    this.getProvinceId(val);
                }, 100);
            },
            getSelectedCity(value) {
                this.user.per_address = value[0] + ',' + value[1];
                this.form.enuser_address = value[0] + ',' + value[1];
                // this.user.city = value[1];
                this.getCityId(value[1]);
            },

            upgradeCompany:function () {
                this.current = false;
            },

            change:function () {
              this.current = !this.current
            },
            uplaodUp:function (e) {
                this.upload(e,1)
            },
            uplaodDown:function (e) {
                this.upload(e,2)
            },
            uplaodPersonalCard:function (e) {
                this.upload(e,3)
            },

            //企业上传相关资料 by jfeng
            uplaodFile1:function (e) {
                this.upload(e,'legal_idcard_up')
            },
            uplaodFile2:function (e) {
                this.upload(e,'legal_idcard_down')
            },
            uplaodFile3:function (e) {
                this.upload(e,'duty_idcard_up')
            },
            uplaodFile4:function (e) {
                this.upload(e,'duty_idcard_down')
            },
            uplaodFile5:function (e) {
                this.upload(e,'license_card')
            },
            TakePictureType: function (mySourceType,type) {
                let that = this;
                that.imgtype =  type;
               navigator.camera.getPicture(function (data){
                let type = that.imgtype;
                let imgs = "data:image/jpeg;base64," + data;
                that.uploadStaer(function(res){
                        if(type==1) {
                            that.user.per_idcard_up = res.data.info;
                        }else if(type==2){
                            that.user.per_idcard_down = res.data.info;
                        }else if(type==3){
                            that.user.personal_with_card = res.data.info;
                        }else if(type == 'legal_idcard_up') {
                            that.form.legal_idcard_up = res.data.info;
                        }else if(type == 'legal_idcard_down') {
                            that.form.legal_idcard_down = res.data.info;
                        }else if(type == 'duty_idcard_up') {
                            that.form.duty_idcard_up = res.data.info;
                        }else if(type == 'duty_idcard_down') {
                            that.form.duty_idcard_down = res.data.info;
                        }else if(type == 'license_card') {
                            that.form.license_card = res.data.info;
                        }

                    },imgs);
                    // if (id == 1) self.imgstr.first = imgs;
                    // if (id == 2) self.imgstr.second = imgs;
                    // if (id == 3) self.imgstr.first1 = imgs;
                    // if (id == 4) self.imgstr.third = imgs;
                    // if (id == 5) self.imgstr.four = imgs;
                    // switch(id){
                    //     case 1:
                    //         self.imgstr.first = imgs;
                    //         self.card_img1 = 'img1';
                    //         console.log(1)
                    //         break;
                    //     case 2:
                    //         self.imgstr.second = imgs;
                    //         self.card_img3 = 'img2';
                    //         console.log(2)
                    //         break;
                    //     case 3:
                    //         self.imgstr.first1 = imgs;
                    //         self.card_img2 = 'img3';
                    //         break;
                    //     case 4:
                    //         self.imgstr.third = imgs;
                    //         self.card_img4 = 'img4';
                    //         break;
                    //     case 5:
                    //         self.imgstr.four = imgs;
                    //         self.card_img5 = 'img5';
                    //         break;
                    // }
                    // self.isShow = '';
                    // // console.log(self.imgstr.first);
                    // self.Http('units/imgstr', {
                    //     imgstr: imgs
                    // }, function (res) {
                    //     layer.loading(false);
                    //     // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1+'^'+res.info;
                    //     // // if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        
                    //     // // if (id == 3) self.form.card_img3 = res.info;
                    //     // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2+'^'+res.info;
                    //     // switch(id){
                    //     //     case 1:
                    //     //     self.img1 = res.info;
                    //     //     self.form.allcard_img1 = res.info;
                    //     //     break;
                    //     //     case 2:
                    //     //     self.img2 = res.info;
                    //     //     self.form.allcard_img2 = self.img2;
                    //     //     break;
                    //     //     case 3:
                    //     //     self.img3 = res.info;
                    //     //     self.form.allcard_img1 = self.img1 +'^'+self.img3;
                    //     //     break;
                    //     //     case 4:
                    //     //     self.img4 = res.info;
                    //     //     self.form.allcard_img2 = self.img2 +'^'+self.img4;
                    //     //     break;
                    //     //     case 5:
                    //     //     self.img5 = res.info;
                    //     //     self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                    //     //     break;
                    //     // }
                    // }, function () {//请求错误
                    //     layer.open({
                    //         content: '服务器响应错误'
                    //         ,skin: 'msg'
                    //         ,time: 1 //2秒后自动关闭
                    //     });
                    //     return;
                    // })
            }, this.onFail, {  
                   quality: 35,  
                   destinationType: Camera.DestinationType.DATA_URL,  
                   encodingType: Camera.EncodingType.JPEG,  
                   sourceType: mySourceType  
               })  

            }, 
            upload:function (e,type) {
                let that = this;
                layer.tips(["照相机","图库"],'',function (e) {
                    if(e == '照相机'){
                       that.TakePictureType(1,type);//调起相机
                    } else {
                       that.TakePictureType(2,type);
                    }
                });

                // if (e.target.files.length <= 0) {
                //     layer.msg('您未选中图片');
                //     return false;
                // }
                // if(e.target.files[0].size/1024 >3000){
                //     layer.msg('请选择小于2M的图片');
                //     return false;
                // }
                let file = e.target.files[0];
                
                layer.loading('上传中...');
                lrz(file,
                {
                    quality:0.1
                })
                .then(function (rst) {
                    // 处理成功会执行
                    // 把处理的好的图片给用户看看呗

                    var img = new Image();
                    img.src = rst.base64; //base64
                    // img.onload = function () {
                    //     document.body.appendChild(img);
                    // };
                    // return rst;
                    that.uploadStaer(function(res){
                        if(type==1) {
                            that.user.per_idcard_up = res.data.info;
                        }else if(type==2){
                            that.user.per_idcard_down = res.data.info;
                        }else if(type==3){
                            that.user.personal_with_card = res.data.info;
                        }else if(type == 'legal_idcard_up') {
                            that.form.legal_idcard_up = res.data.info;
                        }else if(type == 'legal_idcard_down') {
                            that.form.legal_idcard_down = res.data.info;
                        }else if(type == 'duty_idcard_up') {
                            that.form.duty_idcard_up = res.data.info;
                        }else if(type == 'duty_idcard_down') {
                            that.form.duty_idcard_down = res.data.info;
                        }else if(type == 'license_card') {
                            that.form.license_card = res.data.info;
                        }

                    },rst.base64);
                })
                // .then(function (rst) {
                //     console.log(rst)
                // })
                .catch(function (err) {
                    console.log(err,3);
                    layer.msg('上传失败')
                    // 处理失败会执行
                })
                .always(function () {
                    // console.log('不管是成功失败，都会执行',4)
                    // 不管是成功失败，都会执行
                });
                // let reader = new FileReader();
                // reader.readAsDataURL(file);
                // reader.onload = function (res) {
                //     that.uploadStaer(function(res){
                //         if(type==1) {
                //             that.user.per_idcard_up = res.data.info;
                //         }else if(type==2){
                //             that.user.per_idcard_down = res.data.info;
                //         }else if(type==3){
                //             that.user.personal_with_card = res.data.info;
                //         }else if(type == 'legal_idcard_up') {
                //             that.form.legal_idcard_up = res.data.info;
                //         }else if(type == 'legal_idcard_down') {
                //             that.form.legal_idcard_down = res.data.info;
                //         }else if(type == 'duty_idcard_up') {
                //             that.form.duty_idcard_up = res.data.info;
                //         }else if(type == 'duty_idcard_down') {
                //             that.form.duty_idcard_down = res.data.info;
                //         }else if(type == 'license_card') {
                //             that.form.license_card = res.data.info;
                //         }

                //     },res.target.result);
                // }
            },
            uploadStaer:function (fn,img) {
                let that = this;
                
                layer.loading('上传中...');
                that.$http.post(units.doname('index.php/index/Toolure/upload'),units.params({
                    imgStr:img
                })).then(function (res) {
                    layer.loading(false);
                    fn&&fn(res)
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            validate:function (fn) {
                let that = this;
                let tips = ['企业名称','注册资金','法人姓名','法人身份证号','法人联系方式','负责人姓名','负责人身份证','负责人联系方式','法人身份证正面照','法人身份证反面照','负责人身份证正面照','负责人身份证反面照','营业执照','工作地点','城市'];
                let from = this.form;
                let num = -1;
                let next = false;
                $.each(from,function (k,value) {
                    value = value.replace(/(^\s*)|(\s*$)/g, "")
                    num++;
                    if(!value) {
                        layer.msg('请检查'+tips[num]);
                        next = true;
                        return false;
                    }
                    if(k == 'en_person_name' || k == 'enuser_name'){
                        var patt = /[\u4e00-\u9fa5]/;
                        if(!patt.test(value)){
                            layer.msg(tips[num]+'只能输入中文,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'en_person_idcard' || k == 'enuser_idcard'){
                        // var pattern = /\d{15}|\d{17}[0-9Xx]/;
                        var pattern = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/
                        console.log(pattern.test(value));
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'en_contact' || k == 'enuser_contact'){
                        var pattern = /^1[3456789]\d{9}$/;
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                });
                fn&&fn(next);
            },
            postData () {
                let that = this;
                this.validate(function (res) {
                    if(!res) {
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=enterprise'),units.params(that.form)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/user/index';
                                })
                            }else{
                                layer.msg(res.data.info)
                            }
                        }, function () {//请求错误
                            layer.open({
                                content: '服务器响应错误'
                                ,skin: 'msg'
                                ,time: 1 //2秒后自动关闭
                            });
                            return;
                        });
                    }
                })
            },
            userPostData:function () {
                let that = this;
                this.userPostValidate(function(next){
                    if(!next){
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=user'),units.params(that.user)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/user/index';
                                })
                            }else{
                                layer.msg(res.data.info)
                            }
                        }, function () {//请求错误
                            layer.open({
                                content: '服务器响应错误'
                                ,skin: 'msg'
                                ,time: 1 //2秒后自动关闭
                            });
                            return;
                        });
                    }
                })
            },
            userPostValidate:function (fn) {
                let tips = ['姓名','身份证号','联系电话','身份证正面','身份证反面','手持身份证','工作地点','城市id'];
                let from = this.user;
                let num = -1;
                let next = false;
                $.each(from,function (k,value) {
                    num++;
                    if(!value) {
                        layer.msg('请检查'+tips[num]);
                        next = true;
                        return false;
                    };
                    if(k == 'per_name')
                    {
                        var patt = /[\u4e00-\u9fa5]/;
                        if(!patt.test(value)){
                            layer.msg(tips[num]+'只能输入中文,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'per_iphone')
                    {
                        var pattern = /^1[3456789]\d{9}$/;
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'per_idcard')
                    {
                        // var pattern = /\d{15}|\d{17}[0-9Xx]/;
                        var pattern = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/;
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                });
                fn&&fn(next);
            },
            provinceList:function () {
                let  that = this;
                that.$http.post(units.host('provinceList', 'Admin'),units.paramsno({
                    switch:'province'
                })).then( function (res) {
                    that.provinces = res.data.info;
                    for (var province of that.provinces) {
                        this.options2.push({label: province.name, cities: [], key:province.id})
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            },

            getProvinceId:function (name) {
                let that = this;
                that.provinceName = name;
                that.$http.post(units.host('getProvinceId', 'Admin'),units.paramsno({
                    province:that.provinceName[0],
                })).then( function (res){
                    that.provinceId = res.data.info.id;
                    this.getCitys();
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            },

            getCityId:function (name) {
                let that = this;
                that.provinceName = name;
                that.$http.post(units.host('getProvinceId', 'Admin'),units.paramsno({
                    province:that.provinceName,
                })).then( function (res){
                    that.user.city_id = res.data.info.id;
                    that.form.city_id = res.data.info.id;
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            },

            getCitys:function () {
                let that = this;
                that.$http.post(units.host('cityList', 'Admin'),units.params({
                    province_id : this.provinceId,
                })).then (function (res) {
                    this.cityDatas = res.data.info;
                    this.provinces.forEach(function(province,key){
                        if (province.id == that.provinceId) {
                            that.cityDatas.forEach(function (city,k) {
                                that.options2[key].cities.push({label:city.name});
                            })
                        }
                    })
                })
            },

            getUser : function () {
                let that = this;

                that.$http.post(units.host('user_new'),units.params({
                    sw : 'info',
                })).then( function (res){
                    if (res.data.info.user_anthen == 1) {
                        that.user = res.data.info.auth
                    }

                    if (res.data.info.user_anthen == 2) {
                        this.current = false;
                        that.form = res.data.info.auth
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            }

        },

        created () {
            units.title.set('会员认证');
            $(document).scrollTop(0)
            this.provinceList();
            this.getUser();
            // console.log('asdasd',this.$route.query.current);
            if (this.$route.query.current) {
                this.current = false
            }
            this.$store.state.header.left = function () {
                location.href = '#/user/index';
            };

        }
    }
</script>