<!--页面css样式-->
<style scoped lang='scss'>
    .resg{
        /*background: #f2f6f7;*/
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
        /* float:left; */
    }
    .titleClass{
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
         background: #fff;
    }
    .cation {
        padding-top: $top;
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
        padding: 0.4rem 0;
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
    .own-select{//个人地址
        width: 40%;
    }
    .com-select{ //企业地址
        width: 40%;
    }
    .messageuser{
        width: 60%!important;
    }
</style>
<template>
    <!--会员认证-->
    <div class="cation">
        <h5 v-if="user.per_name.length<=0 && form.en_name.length<=0 ">填写认证信息</h5>
        <h5 v-if="($route.query.iswrite&&user.reason) || ($route.query.iswrite&&form.reason)" style="color:red">{{userInfo.auth.reason}}</h5>
        <div class="nav" v-show="user.per_name.length<=0 && form.en_name.length<=0">
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
                                    <input v-if="formShowInfo.en_name" v-model="formShowInfo.en_name" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.en_name" type="text" class="text" placeholder="" >
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>注册资金</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.en_regmoney" v-model="formShowInfo.en_regmoney" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else="formShowInfo.en_regmoney" v-model="formShowInfo.en_regmoney" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>法人姓名</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.en_person_name" v-model="formShowInfo.en_person_name" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.en_person_name" type="text" class="text" placeholder="">

                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.en_person_idcard" v-model="formShowInfo.en_person_idcard" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.en_person_idcard" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.en_contact" v-model="formShowInfo.en_contact" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.en_contact" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="member">
                <h6>负责人资料</h6>
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>负责人</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.enuser_name" v-model="formShowInfo.enuser_name" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.enuser_name" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.enuser_idcard" v-model="formShowInfo.enuser_idcard" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.enuser_idcard" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="formShowInfo.enuser_contact" v-model="formShowInfo.enuser_contact" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="formShowInfo.enuser_contact" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <!-- <li>
                            <a>
                                <label>工作地址</label>
                                <span class="arrow_right"></span>
                                <span class="message">
                                    <input v-model="form.enuser_address" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li> -->
                        <li class="sizePosition">
                            <a>
                                <label>工作地址</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if='addressComFlag' v-model="formShowInfo.enuser_address" type="text" class="text messageuser" placeholder="" disabled >
                                    <el-cascader style="line-height:1.1rem;"
                                        v-if="userInfo.user_anthen == -2"
                                        :class="{'com-select':addressComFlag}"
                                        :style="{lineHeight:'1.1rem'}"

                                        :options="options2"
                                        @active-item-change="handleItemChange"
                                        :props="props"
                                        @change = "getSelectedCity"
                                    >
                                    </el-cascader>
                                </span>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>

            <div class="member">
                <h6  class="per-info">企业信息录入</h6>
                <div  class="prompt">请上传认证所需要资料，以便顺利通过审核，上传信息及照片仅供平台审核使用，请放心上传</div>
                <div class="denity clearfix">
                    <h6 class="titleClass info-title">
                            营业执照
                    </h6>
                    <div class="personalWithCard" v-if='formShowInfo.en_person_name&&!isDisabled' @click="uplaodFile5">
                        <img :src="host+formShowInfo.license_card" v-if="formShowInfo.license_card">
                        <img src="../assets/img/license.png" v-else>
                        <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile5" class="license_file"> -->
                    </div>
                    <div class="personalWithCard" v-else>
                        <img :src="host+formShowInfo.license_card" v-if="formShowInfo.license_card">
                        <img src="../assets/img/license.png" v-else>
                        <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile5" class="license_file"> -->
                    </div>
                    <h6 class="titleClass info-title" >
                        法人身份证
                    </h6>
                    <ul>
                        <li class="cardUpPosition" v-if='formShowInfo.en_person_name&&!isDisabled' @click="uplaodFile1">
                            <img :src="host+formShowInfo.legal_idcard_up" v-if="formShowInfo.legal_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile1" class="legal_file_up"> -->
                        </li>
                         <li class="cardUpPosition" v-else>
                            <img :src="host+formShowInfo.legal_idcard_up" v-if="formShowInfo.legal_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile1" class="legal_file_up"> -->
                        </li>
                        <li class="cardDownPosition" v-if='formShowInfo.en_person_name&&!isDisabled'  @click="uplaodFile2">
                            <img :src="host+formShowInfo.legal_idcard_down" v-if="formShowInfo.legal_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input type="file" @change="uplaodFile2" class="legal_file_down"> -->
                        </li>
                         <li class="cardDownPosition" v-else>
                            <img :src="host+formShowInfo.legal_idcard_down" v-if="formShowInfo.legal_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile2" class="legal_file_down"> -->
                        </li>
                    </ul>
                    <h6 class="titleClass info-title" >
                        负责人身份证
                    </h6>
                    <ul>
                        
                        <li class="cardUpPosition" v-if='formShowInfo.en_person_name&&!isDisabled'   @click="uplaodFile3">
                            <img :src="host+formShowInfo.duty_idcard_up" v-if="formShowInfo.duty_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile3" class="duty_file_up"> -->
                        </li>
                        <li class="cardUpPosition" v-else>
                            <img :src="host+formShowInfo.duty_idcard_up" v-if="formShowInfo.duty_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <inputtype="file" @change="uplaodFile3" class="duty_file_up"> -->
                        </li>
                        <li class="cardDownPosition" v-if='formShowInfo.en_person_name&&!isDisabled'  @click="uplaodFile4">
                            <img :src="host+formShowInfo.duty_idcard_down" v-if="formShowInfo.duty_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile4" class="duty_file_down"> -->
                        </li>
                        <li class="cardDownPosition" v-else>
                            <img :src="host+formShowInfo.duty_idcard_down" v-if="formShowInfo.duty_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input v-if='formShowInfo.en_person_name&&!isDisabled' type="file" @change="uplaodFile4" class="duty_file_down"> -->
                        </li>
                    </ul>
                </div>
            </div>
            <div class="sub_btn">
                <a v-if="form.locationHref" @click="upgradeCompany"  style="background:red;">{{form.showButton}}</a> <!-- 企业审核失败 -->
                        
                <a v-if='!form.locationHref&&form.showButton' style="background:red;">{{form.showButton}}</a> <!-- 企业审核中-->

                <!-- <a v-if="!formShowInfo.en_name" @click="postData">保存</a> -->
            </div>
            <!-- <div v-if="!formShowInfo.en_name" class="foot">请上传认证所需要资料，以便顺利通过审核，上传信息及照片仅供平台审核使用，请放心上传</div> -->
        </div>
        <!-- 企业结束 -->
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
                                    <input v-if="userShowInfo.per_name" v-model="userShowInfo.per_name" type="text" class="text" placeholder="" :disabled ='isDisabled' >
                                    <input v-else v-model="userShowInfo.per_name" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="userShowInfo.per_idcard" v-model="userShowInfo.per_idcard" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="userShowInfo.per_idcard" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系电话</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="userShowInfo.per_iphone" v-model="userShowInfo.per_iphone" type="text" class="text" placeholder="" :disabled ='isDisabled'>
                                    <input v-else v-model="userShowInfo.per_iphone" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li class="sizePosition sizePositionown">
                            <a class='own-address'>
                                <label>工作地址</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="addressFlag" v-model="userShowInfo.per_address" type="text" class="text messageuser" placeholder="" disabled>
                                    <!-- <input v-else v-model="userShowInfo.per_address" type="text" class="text" placeholder="" > -->
                                    <el-cascader 
                                        v-if="userInfo.user_anthen == -1 || userInfo.user_anthen == -2"
                                        :class="{'own-select':addressFlag}"
                                        :style="{lineHeight:'1.1rem'}"
                                        
                                        :options="options2"
                                        @active-item-change="handleItemChange"
                                        :props="props"
                                        @change = "getSelectedCity"
                                >
                                </el-cascader>
                                </span>
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
                        <li class="personal_up" v-if="userShowInfo.per_name&&!isDisabled"  @click="uplaodUp">
                            <img :src="host+userShowInfo.per_idcard_up" v-if="userShowInfo.per_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodUp" class="file_up"> -->
                        </li>
                        <li class="personal_up" v-else>
                            <img :src="host+userShowInfo.per_idcard_up" v-if="userShowInfo.per_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodUp" class="file_up"> -->
                        </li>
                        <li class="personal_down" v-if="userShowInfo.per_name&&!isDisabled"  @click="uplaodDown">
                            <img :src="host+userShowInfo.per_idcard_down" v-if="userShowInfo.per_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodDown" class="file_down"> -->
                        </li>
                        <li class="personal_down" v-else>
                            <img :src="host+userShowInfo.per_idcard_down" v-if="userShowInfo.per_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodDown" class="file_down"> -->
                        </li>
                    </ul>
                    <div class="resg" >
                        请上传您的半身手持身份证照。
                    </div>
                    <div class="personalWithCard" v-if="userShowInfo.per_name&&!isDisabled" @click="uplaodPersonalCard">
                        <img :src="host+userShowInfo.personal_with_card" v-if="userShowInfo.personal_with_card">
                        <img src="../assets/img/self_card.png" v-else>
                        <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodPersonalCard"> -->
                    </div>
                    <div class="personalWithCard" v-else>
                        <img :src="host+userShowInfo.personal_with_card" v-if="userShowInfo.personal_with_card">
                        <img src="../assets/img/self_card.png" v-else>
                        <!-- <input v-if="userShowInfo.per_name&&!isDisabled" type="file" @change="uplaodPersonalCard"> -->
                    </div>
                </div>
                <div class="sub_btn sub_btn2"> 
                    <a v-if="user.locationHref" @click="upgradeCompany"  style="background:red;">{{user.showButton}}</a> <!-- 个人审核失败 -->
                        
                    <a v-if="!user.locationHref&&user.showButton" style="background:red;">{{user.showButton}}</a> <!-- 个人审核中-->

                    <!-- <a v-if="!user.per_name && !form.en_name" @click="userPostData">提交信息</a> -->
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
                formShowInfo:{ //企业展示数据
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
                userShowInfo: {//个人展示信息
                    per_name:'',
                    per_idcard:'',
                    per_iphone:'',
                    per_idcard_up:'',
                    per_idcard_down:'',
                    personal_with_card:'',
                    per_address:'',
                    city_id : '',
                },
                userInfo: {}, //所有信息
                current:true,
                host:units.getHost(),
                provinces:{},
                provinceId:'',
                provinceName:'',
                cityDatas:{},   
                isDisabled: true, //判断是否可读写

                //级联选择器组件 by jfeng
                options2: [],
                props: {
                    value: 'label',
                    children: 'cities'
                },
                addressFlag: true,//个人地址是否显示
                addressComFlag: true, //企业地址select是否出现
                // selectedOptions2: ['北京市','东城区']
            }
        },
        methods: {
            handleItemChange(val) {
                setTimeout(_ => {
                    this.getProvinceId(val);
                }, 100);
            },
            getSelectedCity(value) {
                
                this.userShowInfo.per_address = value[0] + ',' + value[1];
                this.formShowInfo.enuser_address = value[0] + ',' + value[1];
                // this.user.city = value[1];
                this.getCityId(value[1]);
            },

            upgradeCompany:function () {
                
                if(this.userInfo.user_anthen == -1 ) { //个人审核失败
                    let that = this;
                    this.userPostValidate(function(next){
                        if(!next){
                        console.log(that.userShowInfo)
                            layer.loading('请稍等...');
                            that.$http.post(units.host('Authentication?type=user'),units.params(that.userShowInfo)).then(function (res) {
                                layer.loading(false);
                                if(res.data.code > 0){
                                    layer.msg('提交成功',2,function () {
                                        location.href = '#/Authentication_detail';
                                        that.addressFlag = true;
                                        that.getUser();
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
                    // location.href="#/Authentication_detail";
                } else if (this.userInfo.user_anthen == -2) {//企业审核失败
                    let that = this;
                    this.validate(function (res) {
                        if(!res) {
                            layer.loading('请稍等...');
                            that.$http.post(units.host('Authentication?type=enterprise'),units.params(that.formShowInfo)).then(function (res) {
                                layer.loading(false);
                                if(res.data.code > 0){
                                    layer.msg('提交成功',2,function () {
                                        location.href = '#/Authentication_detail';
                                        that.addressComFlag = true;
                                        that.getUser();
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
                    // location.href="#/Authentication_detail";
                } else if(this.userInfo.user_anthen == 1) {//升级企业认证
                    this.current = false;
                    location.href="#/Authentication?current='detail'"
                } else {
                    layer.msg(this.userInfo.warning);
                    return;
                }
            },

            change:function () {
              this.current = !this.current
            },
            uplaodUp:function (e) {//个人身份证正面
                this.upload(e,1) 
            },
            uplaodDown:function (e) {//个人身份证反面
                this.upload(e,2)
            },
            uplaodPersonalCard:function (e) {//个人手持身份证照片
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
                // // if(e.target.files[0].size/1024 >3000){
                // //     layer.msg('请选择小于2M的图片');
                // //     return false;
                // // }
                // let file = e.target.files[0];
                // // let reader = new FileReader();
                // // reader.readAsDataURL(file);
                // layer.loading('上传中...');
                // lrz(file,
                // {
                //     quality:0.1
                // })
                // .then(function (rst) {
                //     // 处理成功会执行
                //     // 把处理的好的图片给用户看看呗

                //     var img = new Image();
                //     img.src = rst.base64; //base64
                //     // img.onload = function () {
                //     //     document.body.appendChild(img);
                //     // };
                //     // return rst;
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

                //     },rst.base64);
                // })
                // // .then(function (rst) {
                // //     console.log(rst)
                // // })
                // .catch(function (err) {
                //     console.log(err,3);
                //     layer.msg('上传失败')
                //     // 处理失败会执行
                // })
                // .always(function () {
                //     // console.log('不管是成功失败，都会执行',4)
                //     // 不管是成功失败，都会执行
                // });
                // reader.onload = function (res) {
                    // that.uploadStaer(function(res){
                    //     if(type==1) {//个人身份证正面
                    //         that.userShowInfo.per_idcard_up = res.data.info;
                    //         console.log(that.userShowInfo.per_idcard_up)
                    //     }else if(type==2){//个人身份证反面
                    //         that.userShowInfo.per_idcard_down = res.data.info;
                    //     }else if(type==3){//个人手持身份证照片
                    //         that.userShowInfo.personal_with_card = res.data.info;
                    //     }else if(type == 'legal_idcard_up') {
                    //         that.formShowInfo.legal_idcard_up = res.data.info;
                    //     }else if(type == 'legal_idcard_down') {
                    //         that.formShowInfo.legal_idcard_down = res.data.info;
                    //     }else if(type == 'duty_idcard_up') {
                    //         that.formShowInfo.duty_idcard_up = res.data.info;
                    //     }else if(type == 'duty_idcard_down') {
                    //         that.formShowInfo.duty_idcard_down = res.data.info;
                    //     }else if(type == 'license_card') {
                    //         that.formShowInfo.license_card = res.data.info;
                    //     }

                    // },res.target.result);
                // }
            },
            uploadStaer:function (fn,img) {
                let that = this;
                // layer.loading('上传中...');
                that.$http.post(units.doname('index.php/index/Toolure/upload'),units.params({
                    imgStr:img
                })).then(function (res) {
                    layer.loading(false);
                    if(res.data.code > 0) fn&&fn(res)
                    else layer.msg(res.data.msg)
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
                let from = that.formShowInfo;
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
                        var pattern = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/;
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                    // if(k == 'en_contact' || k == 'enuser_contact'){
                    //     if(value.length != 11){
                    //         layer.msg(tips[num]+'输入有误,请检查');
                    //         next = true;
                    //         return false;
                    //     }
                    // }
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
            postData(){ //企业提交
                let that = this;
                this.validate(function (res) {
                    if(!res) {
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=enterprise'),units.params(that.form)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/';
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
            userPostData:function () { //个人
                let that = this;
                this.userPostValidate(function(next){
                    if(!next){
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=user'),units.params(that.user)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/';
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
                let from = this.userShowInfo;
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
                    // if(k == 'per_iphone')
                    // {
                    //     if(value.length != 11){
                    //         layer.msg(tips[num]+'输入有误,请检查');
                    //         next = true;
                    //         return false;
                    //     }
                    // }
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
            provinceList:function () { //省份数据
                let  that = this;
                that.$http.post(units.host('provinceList', 'Admin'),units.paramsno({
                    switch:'province'
                })).then( function (res) {
                    that.provinces = res.data.info;
                    for (var province of that.provinces) {
                        this.options2.push({label: province.name, value: province.name,cities: [], key:province.id,children: []});
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
                that.$http.post(units.host('cityList', 'Admin'),units.paramsno({
                    province_id : this.provinceId,
                })).then (function (res) {
                    this.cityDatas = res.data.info;
                    this.provinces.forEach(function(province,key){
                        if (province.id == that.provinceId) {
                            if (that.userInfo.user_anthen == -1) {
                                that.addressFlag = false;//个人让原来渲染的地址隐藏
                            } else if(that.userInfo.user_anthen == -2) {
                                that.addressComFlag = false;//企业让原来渲染的地址隐藏
                            }
                            

                            that.cityDatas.forEach(function (city,k) {
                                that.options2[key].cities.push({label:city.name, value: city.name});
                                that.options2[key].children.push({label:city.name, value: city.name});
                            })
                        }
                    })
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            },

            getUser : function () {
                let that = this;

                that.$http.post(units.host('user_new'),units.params({
                    sw : 'info',
                })).then( function (res){
                    that.userInfo = res.data.info;
                    that.isDisabled = true;
                    if (res.data.info.user_anthen < 3) {
                        //user_anthen以前 ==>    -1、企业认证失败1、个人认证  2、企业认证审核中   3、企业认证


                        //20180424 user_anthen:  0未认证,1 个人已认证,2企业已认证，
                        // 3个人认证审核（不能点击），4，企业认证审核中(不能点击)
                        // -1个人认证失败（个人认证详情编辑页） -2 企业认证失败（企业认证详情编辑页）
                    }
                    if (res.data.info.user_anthen == 1 || res.data.info.user_anthen == 3 || res.data.info.user_anthen == -1) { //个人数据
                        that.user = res.data.info.auth;
                        

                        that.userShowInfo.per_name = res.data.info.auth.per_name;//个人展示信息
                        that.userShowInfo.per_idcard = res.data.info.auth.per_idcard;
                        that.userShowInfo.per_iphone = res.data.info.auth.per_iphone;
                        that.userShowInfo.per_idcard_up = res.data.info.auth.per_idcard_up;
                        that.userShowInfo.per_idcard_down = res.data.info.auth.per_idcard_down;
                        that.userShowInfo.personal_with_card = res.data.info.auth.personal_with_card;
                        that.userShowInfo.per_address = res.data.info.auth.per_address;
                        that.userShowInfo.city_id = res.data.info.auth.city_id;
                    }

                    if (res.data.info.user_anthen == 2 || res.data.info.user_anthen == 4 || res.data.info.user_anthen == -2) {//企业数据
                        this.current = false;
                        that.form = res.data.info.auth;

                        //企业展示数据
                        that.formShowInfo.en_name = res.data.info.auth.en_name;
                        that.formShowInfo.en_regmoney = res.data.info.auth.en_regmoney;
                        that.formShowInfo.en_person_name = res.data.info.auth.en_person_name;
                        that.formShowInfo.en_person_idcard = res.data.info.auth.en_person_idcard;
                        that.formShowInfo.en_contact = res.data.info.auth.en_contact;
                        that.formShowInfo.enuser_name = res.data.info.auth.enuser_name;
                        that.formShowInfo.enuser_idcard = res.data.info.auth.enuser_idcard;
                        that.formShowInfo.enuser_contact = res.data.info.auth.enuser_contact;
                        that.formShowInfo.legal_idcard_up = res.data.info.auth.legal_idcard_up;
                        that.formShowInfo.legal_idcard_down = res.data.info.auth.legal_idcard_down;
                        that.formShowInfo.duty_idcard_up = res.data.info.auth.duty_idcard_up;
                        that.formShowInfo.duty_idcard_down = res.data.info.auth.duty_idcard_down;
                        that.formShowInfo.license_card = res.data.info.auth.license_card;
                        that.formShowInfo.enuser_address = res.data.info.auth.enuser_address;
                        that.formShowInfo.city_id = res.data.info.auth.city_id;
                    }
                    if (this.$route.query.iswrite) { //判断是否可读写
                    console.log(111)
                        that.isDisabled = false;
                    } else {
                        console.log(222)
                        that.isDisabled = true;
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
        updated () {
            this.$store.state.header.left = function () {
                location.href = '#/user/index';
            };
        },
        mounted () {
            this.getUser();
        },
        created () {
            units.title.set('会员认证');
            this.provinceList();
            
            this.$store.state.header.left = function () {
                location.href = '#/user/index';
            };
        }
    }
</script>