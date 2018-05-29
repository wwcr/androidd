<template>
    <!--找车服务-->
    <div id="Findcar">
        <div v-if='form.card_brand&&fail_reason' class="resg" style="color:red;font-size: .5rem;">
            {{fail_reason?fail_reason:'请填写真实信息，以便我们寻找车辆'}}
        </div>
        <div v-else class="resg">
            请如实填写需寻找车辆信息，本平台只提供寻车服务，该信息不做它用，请放心上传！
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <label>车辆品牌</label>
                        <span @click="carBrand('/api/brand')">
                            <!-- <span class="arrow_right_only"></span> -->
                            <span class="message">
                                <input 
                                    type="text" 
                                    unselectable="on" onfocus="this.blur()"
                                    readonly 
                                    v-model="form.card_brand" 
                                    class="text"
                                    placeholder="请选择车辆品牌">
                            </span>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>车辆号码</label>
                        <!-- <span class="arrow_right_2"></span> -->
                        <span class="message" style="position:relative">
                          <input  
                            class="text" 
                            type="text" 
                            v-model="form.card_allnumber"
                            placeholder="请输入车牌号码"
                            style="margin-left: 1.61rem;">
                            <div class="aui-list-item-input"
                                 style="position:absolute;top:0rem;width:1.6rem;overflow:hidden">
                                <select class="select-dom" autocomplete="off" v-model="form.card_number">
                                    <option value="京" selected="selected">京</option>
                                    <option v-if="index>0" v-for="(x,index) in cardata"
                                            :value="x.j"
                                            :key='index'
                                            :index="index">{{x.j}}</option>
                                </select>
                            </div>
                        </span>
                    </a>
                </li>
                
                <li>
                    <a>
                        <label>车辆颜色</label>
                        <!-- <span class="arrow_right_only"></span> -->
                        <span class="message">
                          <input 
                            class="text"
                            type="text" 
                            v-model="form.card_color" 
                            placeholder="请填写车辆颜色">
                        </span>
                    </a>
                </li>
                
            </ul>
        </div>
        <!-- 机动车登记图片开始 -->
        <div class="pledge img-page">
            <div class='license-title'>机动车登记图片</div>
            <div class="license-ul1">
                <div class="li">
                    <div class="img-box" v-model='card_img1' @click='zoom(1)'><div class="img-mark" v-show='isShow == card_img1'></div><img :src="imgstr.first" v-if="imgstr.first"></div>
                    <!-- <div class="upload-btn"><input type="file" accept="image/*" capture='camera' @change="upload(1)"></div> -->
                    <div class="upload-btn" @click="upload(1)"></div>
                </div>
                <div class="li">
                    <div class="img-box"  v-model='card_img2' @click='zoom(3)'><div class="img-mark" v-show='isShow == card_img2'></div><img :src="imgstr.first1" v-if="imgstr.first1"></div>
                    <!-- <div class="upload-btn"><input type="file" accept="image/*" capture='camera' @change="upload(3)"></div> -->
                     <div class="upload-btn" @click="upload(3)"></div>
                </div>
                <div class="li"></div>
            </div>
            <!-- 机动车登记图片结束 -->
            <!-- 签约合同图片开始 -->
            <div class='license-title' style="margin-top: .4rem;">签约合同图片</div>
            <div class="license-ul1">
                <div class="li">
                    <div class="img-box"  v-model='card_img3' @click='zoom(2)'><div class="img-mark" v-show='isShow == card_img3'></div><img :src="imgstr.second" v-if="imgstr.second"></div>
                    <!-- <div class="upload-btn"><input type="file" accept="image/*" capture='camera' @change="upload(2)"></div> -->
                    <div class="upload-btn" @click="upload(2)"></div>
                </div>
                <div class="li">
                    <div class="img-box"  v-model='form.card_img4' @click='zoom(4)'><div class="img-mark" v-show='isShow ==card_img4'></div><img :src="imgstr.third" v-if="imgstr.third"></div>
                    <!-- <div class="upload-btn"><input type="file" accept="image/*" capture='camera' @change="upload(4)"></div> -->
                    <div class="upload-btn" @click="upload(4)"></div>
                </div>
                <div class="li">
                    <div class="img-box" v-model='form.card_img5' @click='zoom(5)'><div class="img-mark" v-show='isShow == card_img5'></div><img :src="imgstr.four" v-if="imgstr.four"></div>
                    <!-- <div class="upload-btn"><input type="file" accept="image/*" capture='camera' @change="upload(5)"></div> -->
                    <div class="upload-btn" @click="upload(5)"></div>
                </div>
            </div>
            <!-- 签约合同图片开始 -->
            <!-- <p class="aptitude" >本次签字后，再次填写则不需再次签署。  签署委托查找合同，并在提供<span class="pact">电子合同</span>手动签字</p> -->
             <!-- @click='contract' -->
        <p class="explain-text">以上资料各上传一张图片即可，上传完整资料可加速审核，如有资料不详请联系客服。客服电话：{{$store.state.phone}}</p>
        </div>
        <div class="sub_btn">
            <a @click="postData">
                <!-- <span v-if="zl">下一步</span> -->
                <span>提&emsp;交</span>
            </a>
            <!-- <p class="pact" style="margin-top: .5rem;" @click='contract'>请点击委托回收协议签字。</p> -->
        </div>
        <!--弹窗-->
        <div class="fixed-ad-layer" style="display: block;" v-if="false">
            <div class="fixed-ad-con">
                <a class="ad-img fixed-ad-img" href="">
                    <img src="../../src/assets/img/img_loding.png">
                    <p class="p1">审核中...</p>
                    <p class="p2">您信息已提交，工作人员正在审核，我们将在12小时内确认信息并通知您。</p>
                </a>
                <div class="close-fixed-ad"></div>
            </div>
        </div>
        <!-- 车牌信息 -->
        <listInfo 
            :brandList='brandList'
            @closeBrand = 'closeBrand'
            ref='detailInfo'
            v-show = 'infoFlag'/>
        <!-- 寻车期限 -->
        <div class="card-time-mark" v-show='timeFlag' ref='mark'>
            <div class="card_contract-box" v-if='timeFlag'>
                <div class="btn-box">
                    <button class="cancel-btn" @click="cancelTime(0)">取消</button>
                    <button class="sure-btn" @click="cancelTime(1)">确定</button>
                </div>
                <mt-picker :slots="slots" @change="onValuesChange"></mt-picker>
            </div>
        </div>
        <!-- 是否GPS -->
        <!-- <GpsPicker
            v-if='gpsFlag'
            @closePicker= 'closePicker'
        /> -->
        <!-- 城市 -->
        <City
            v-if='cityFlag'
            @closeCity='closeCity'
        />
    </div>
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    import lrz from '../../static/lrz/lrz.bundle'
    import listInfo from '@/components/frame/indexList'
    import City from '@/components/find/city'
    import scroll from '../../static/mobiscroll/js/mobiscroll.jquery.min'
    import Vue from 'vue'
    import { Picker } from 'mint-ui';
    Vue.component(Picker.name, Picker);
    import GpsPicker from '@/components/frame/gpsPicker'
    export default {
        name: 'index',
        data() {
            return {
                form: {
                    card_brand: '', //车辆品牌
                    card_number: '京', //车牌号码
                    card_allnumber:'', //车牌后6位
                    // card_city: '', //城市
                    card_color: '',//车辆颜色
                    // card_contract: '', //寻车期限
                    allcard_img1:'',
                    allcard_img2:'',
                    // : '',
                    // type: cookie.get('sign_uesr')
                    // gps: 1 //1没有GPS，2有GPS 
                },
                reFindCarData: {},//重新审核数据
                fail_reason: '',//错误信息
                card_img1: '',
                card_img3: '',
                card_img2: '',  //图片
                card_img4: '',  //图片
                card_img5: '',  //图片
                gps: {
                    platform: '',
                    user: '',
                    pwd: ''
                },
                imgstr: {
                    // 机动车
                    first: require('../assets/img/jd-car1.jpg'),
                    first1: require('../assets/img/jd-car2.jpg'),
                    // 签约合同
                    second: require('../assets/img/jd-car2.jpg'),
                    third: require('../assets/img/jd-car2.jpg'),
                    four: require('../assets/img/jd-car2.jpg'),
                    // five:'',
                },
                card: {
                    card_brand: 0
                },
                gpsVal: '否',
                cardata:{},
                cards:'',
                zl:'',
                car_ass_id: '',//车辆品牌ID
                img1:'',
                img2:'',
                img3:'',
                img4:'',
                img5:'',
                infoData: [],
                cityFlag: false,//疑似城市开关
                infoFlag: false,
                brandList: [],//车牌数据
                timeFlag: false, //寻车期限开关，
                gpsFlag: false, //gps开关,
                gpsShow: false, //是否显示gps信息
                contractFlag: true,
                isShow: '', //是否显示图片遮罩
                slots: [ //寻车期限(mint-ui)
                    {
                        flex: 1,
                        values: [ '3月','6月', '9月','12月'],
                        className: 'slot1',
                        textAlign: 'center'
                    }
                ],
                imgUid: '',
            }
        },
        watch:{
            'form.card_allnumber':function () {
                if(this.form.card_allnumber) {
                    this.form.card_allnumber = this.form.card_allnumber.toUpperCase()
                }
            }
        },
        methods: {
            validate: function (fn, midia) {
                let flag = true;
                // let midia = $('input').not('.gps-page input');
                console.log(midia.eq(0).attr('placeholder'))
                let len = midia.length;
                for (var i = 0; i < len; i++) {
                    if (!midia.eq(i).val()) {
                        let tips = midia.eq(i).attr('placeholder');
                        layer.msg(tips);
                        flag = false;
                        break;
                    }
                }
                fn && fn(flag);
            },
            postData() { //提交委单
                console.log(this.form, 121212)
                let that = this;
                let tips = ['车辆品牌', '车辆号码','车辆号码','车辆颜色','机动车登记图片', '签约合同图片'];
                let from = this.form;
                let num = -1;
                let next = false;
                $.each(from, function (k, value) {
                    num++;
                    if (!value) {
                        // console.log(value);
                        layer.msg('请检查' + tips[num]);
                        next = true;
                        return false;
                    }
                });
                if (next) return false;

                if(!units.isVehicleNumber(this.form.card_allnumber)){//判断车牌格式是否匹配
                    layer.msg('请填写正确的车牌格式');
                    return false;
                } else {
                    // if(this.form.card_color.length > 4) { //判断车辆的颜色
                    //     layer.msg('请填写正确的车辆颜色');
                    //     return;
                    // }
                    // if (cookie.get('c_status')  == 0) {//没签合同 把表单信息保存起来 ==>以后可能使用
                        cookie.set('findCarForm', JSON.stringify(this.form));
                    //     this.$router.push('contract');
                    //     return false;
                    // }
                    let find_id = that.$route.query.find_id*1;
                    if(find_id){
                        this.$http.post(units.host('findcarnew'), units.params({
                            card_brand: this.form.card_brand, //车辆品牌
                            card_number: this.form.card_number, //车牌号码
                            card_allnumber:this.form.card_allnumber, //车牌后6位
                            card_color: this.form.card_color,//车辆颜色
                            allcard_img1:this.form.allcard_img1,
                            allcard_img2:this.form.allcard_img2,
                            find_id:find_id
                        })).then(function (res) {
                            console.log(res,find_id)
                            if (res.data.code > 0) {
                                layer.msg(res.data.msg, 2, function () {
                                    cookie.del('findCarForm');
                                    cookie.del('cards');
                                        location.href= '#/server/content';
                                })
                            } else if(res.data.code == 0){ //请求失败提醒
                                layer.msg(res.data.msg);
                                return;
                            }
                        }, function () {//请求错误
                            layer.open({
                                content: '服务器响应错误'
                                ,skin: 'msg'
                                ,time: 1 //2秒后自动关闭
                            });
                            return;
                        });
                    } else {
                        this.$http.post(units.host('findcarnew'), units.params(this.form)).then(function (res) {
                            if (res.data.code > 0) {
                                layer.msg(res.data.msg, 2, function () {
                                    cookie.del('findCarForm');
                                    cookie.del('cards');
                                    // if(cookie.get('sign_uesr') == 2) {
                                        // location.href= '#/carnurse/success';
                                    // } else {  
                                        location.href= '#/carnurse/success';
                                    // }
                                    // if(that.zl == 'send'){
                                    //     location.href = '#/server/terrace?id='+res.data.msg
                                    // }else{
                                    //     console.log(res.data.code)
                                    //     that.href('pay?type=2&order=' + res.data.code)
                                    // }
                                })
                            } else if(res.data.code == 0){
                                layer.msg(res.data.msg);
                                return;
                            }
                        },function () {//请求错误
                            layer.open({
                                content: '服务器响应错误'
                                ,skin: 'msg'
                                ,time: 1 //2秒后自动关闭
                            });
                            return;
                        });
                    }
     
                }
            },
            onSuccess(data,id){
                console.log(data);
                console.log(id);
                let self = this;
                // let id = 1;
                   let imgs = "data:image/jpeg;base64," + data;
                    // if (id == 1) self.imgstr.first = imgs;
                    // if (id == 2) self.imgstr.second = imgs;
                    // if (id == 3) self.imgstr.first1 = imgs;
                    // if (id == 4) self.imgstr.third = imgs;
                    // if (id == 5) self.imgstr.four = imgs;
                    switch(id){
                        case 1:
                            self.imgstr.first = imgs;
                            self.card_img1 = 'img1';
                            console.log(1)
                            break;
                        case 2:
                            self.imgstr.second = imgs;
                            self.card_img3 = 'img2';
                            console.log(2)
                            break;
                        case 3:
                            self.imgstr.first1 = imgs;
                            self.card_img2 = 'img3';
                            break;
                        case 4:
                            self.imgstr.third = imgs;
                            self.card_img4 = 'img4';
                            break;
                        case 5:
                            self.imgstr.four = imgs;
                            self.card_img5 = 'img5';
                            break;
                    }
                    self.isShow = '';
                    // console.log(self.imgstr.first);
                    self.Http('units/imgstr', {
                        imgstr: imgs
                    }, function (res) {
                        layer.loading(false);
                        // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1+'^'+res.info;
                        // // if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        
                        // // if (id == 3) self.form.card_img3 = res.info;
                        // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2+'^'+res.info;
                        switch(id){
                            case 1:
                            self.img1 = res.info;
                            self.form.allcard_img1 = res.info;
                            break;
                            case 2:
                            self.img2 = res.info;
                            self.form.allcard_img2 = self.img2;
                            break;
                            case 3:
                            self.img3 = res.info;
                            self.form.allcard_img1 = self.img1 +'^'+self.img3;
                            break;
                            case 4:
                            self.img4 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4;
                            break;
                            case 5:
                            self.img5 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                            break;
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
            onFail(data){
                console.log(data);
            },
             TakePictureType: function (mySourceType,id) {
                let self = this;
                self.imgUid =  id;
               navigator.camera.getPicture(function (data){
                let id = self.imgUid;
                let imgs = "data:image/jpeg;base64," + data;
                    // if (id == 1) self.imgstr.first = imgs;
                    // if (id == 2) self.imgstr.second = imgs;
                    // if (id == 3) self.imgstr.first1 = imgs;
                    // if (id == 4) self.imgstr.third = imgs;
                    // if (id == 5) self.imgstr.four = imgs;
                    switch(id){
                        case 1:
                            self.imgstr.first = imgs;
                            self.card_img1 = 'img1';
                            console.log(1)
                            break;
                        case 2:
                            self.imgstr.second = imgs;
                            self.card_img3 = 'img2';
                            console.log(2)
                            break;
                        case 3:
                            self.imgstr.first1 = imgs;
                            self.card_img2 = 'img3';
                            break;
                        case 4:
                            self.imgstr.third = imgs;
                            self.card_img4 = 'img4';
                            break;
                        case 5:
                            self.imgstr.four = imgs;
                            self.card_img5 = 'img5';
                            break;
                    }
                    self.isShow = '';
                    // console.log(self.imgstr.first);
                    self.Http('units/imgstr', {
                        imgstr: imgs
                    }, function (res) {
                        layer.loading(false);
                        // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1+'^'+res.info;
                        // // if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        
                        // // if (id == 3) self.form.card_img3 = res.info;
                        // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2+'^'+res.info;
                        switch(id){
                            case 1:
                            self.img1 = res.info;
                            self.form.allcard_img1 = res.info;
                            break;
                            case 2:
                            self.img2 = res.info;
                            self.form.allcard_img2 = self.img2;
                            break;
                            case 3:
                            self.img3 = res.info;
                            self.form.allcard_img1 = self.img1 +'^'+self.img3;
                            break;
                            case 4:
                            self.img4 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4;
                            break;
                            case 5:
                            self.img5 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                            break;
                        }
                    }, function () {//请求错误
                        layer.open({
                            content: '服务器响应错误'
                            ,skin: 'msg'
                            ,time: 1 //2秒后自动关闭
                        });
                        return;
                    })
            }, this.onFail, {  
                   quality: 50,  
                   destinationType: Camera.DestinationType.DATA_URL,  
                   encodingType: Camera.EncodingType.JPEG,  
                   sourceType: mySourceType  
               })  

            },  
            //上传图片
            upload: function (id) {
                let self = this;
                layer.tips(["照相机","图库"],'',function (e) {
                    if(e == '照相机'){
                       self.TakePictureType(1,id);//调起相机
                    } else {
                        self.TakePictureType(2,id);
                    }
                });
                // // alert(id);
                // if (event.target.files.length <= 0) {
                //     layer.msg('您未选中图片');
                //     return false;
                // }
                // let file = event.target.files[0];
                // // if(event.target.files[0].size/1024 >3000){
                // //     layer.msg('请选择小于2M的图片');
                // //     return false;
                // // }
                // layer.loading('上传中...');
                // // let reader = new FileReader();
                // // reader.readAsDataURL(event.target.files[0]);
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
                //     let imgs = rst.base64;
                //     // if (id == 1) self.imgstr.first = imgs;
                //     // if (id == 2) self.imgstr.second = imgs;
                //     // if (id == 3) self.imgstr.first1 = imgs;
                //     // if (id == 4) self.imgstr.third = imgs;
                //     // if (id == 5) self.imgstr.four = imgs;
                //     switch(id){
                //     	case 1:
	               //      	self.imgstr.first = imgs;
                //             self.card_img1 = 'img1';
                //             console.log(1)
	               //      	break;
                //     	case 2:
	               //      	self.imgstr.second = imgs;
                //             self.card_img3 = 'img2';
                //             console.log(2)
	               //      	break;
                //     	case 3:
	               //      	self.imgstr.first1 = imgs;
	               //      	self.card_img2 = 'img3';
	               //      	break;
	               //      case 4:
	               //      	self.imgstr.third = imgs;
                //     		self.card_img4 = 'img4';
                //     		break;
                //     	case 5:
                //     		self.imgstr.four = imgs;
                //     		self.card_img5 = 'img5';
                //     		break;
                //     }
                //     self.isShow = '';
                //     // console.log(self.imgstr.first);
                //     self.Http('units/imgstr', {
                //         imgstr: imgs
                //     }, function (res) {
                //         layer.loading(false);
                //         // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1+'^'+res.info;
                //         // // if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        
                //         // // if (id == 3) self.form.card_img3 = res.info;
                //         // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2+'^'+res.info;
                //         switch(id){
                //             case 1:
                //             self.img1 = res.info;
                //             self.form.allcard_img1 = res.info;
                //             break;
                //             case 2:
                //             self.img2 = res.info;
                //             self.form.allcard_img2 = self.img2;
                //             break;
                //             case 3:
                //             self.img3 = res.info;
                //             self.form.allcard_img1 = self.img1 +'^'+self.img3;
                //             break;
                //             case 4:
                //             self.img4 = res.info;
                //             self.form.allcard_img2 = self.img2 +'^'+self.img4;
                //             break;
                //             case 5:
                //             self.img5 = res.info;
                //             self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                //             break;
                //         }
                //     }, function () {//请求错误
                //         layer.open({
                //             content: '服务器响应错误'
                //             ,skin: 'msg'
                //             ,time: 1 //2秒后自动关闭
                //         });
                //         return;
                //     })
                //     // that.uploadStaer(function(res){
                //     //     if(type==1) {
                //     //         that.user.per_idcard_up = res.data.info;
                //     //     }else if(type==2){
                //     //         that.user.per_idcard_down = res.data.info;
                //     //     }else if(type==3){
                //     //         that.user.personal_with_card = res.data.info;
                //     //     }else if(type == 'legal_idcard_up') {
                //     //         that.form.legal_idcard_up = res.data.info;
                //     //     }else if(type == 'legal_idcard_down') {
                //     //         that.form.legal_idcard_down = res.data.info;
                //     //     }else if(type == 'duty_idcard_up') {
                //     //         that.form.duty_idcard_up = res.data.info;
                //     //     }else if(type == 'duty_idcard_down') {
                //     //         that.form.duty_idcard_down = res.data.info;
                //     //     }else if(type == 'license_card') {
                //     //         that.form.license_card = res.data.info;
                //     //     }

                //     // },rst.base64);
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
                // reader.onload = function (e) {
                //     let imgs = this.result;
                //     // if (id == 1) self.imgstr.first = imgs;
                //     // if (id == 2) self.imgstr.second = imgs;
                //     // if (id == 3) self.imgstr.first1 = imgs;
                //     // if (id == 4) self.imgstr.third = imgs;
                //     // if (id == 5) self.imgstr.four = imgs;
                //     switch(id){
                //     	case 1:
	            //         	self.imgstr.first = imgs;
	            //         	self.card_img1 = 'img1';
	            //         	break;
                //     	case 2:
	            //         	self.imgstr.second = imgs;
	            //         	self.card_img3 = 'img2';
	            //         	break;
                //     	case 3:
	            //         	self.imgstr.first1 = imgs;
	            //         	self.card_img2 = 'img3';
	            //         	break;
	            //         case 4:
	            //         	self.imgstr.third = imgs;
                //     		self.card_img4 = 'img4';
                //     		break;
                //     	case 5:
                //     		self.imgstr.four = imgs;
                //     		self.card_img5 = 'img5';
                //     		break;
                //     }
                //     this.isShow = imgs
                //     // console.log(self.imgstr.first);
                //     self.Http('units/imgstr', {
                //         imgstr: imgs
                //     }, function (res) {
                //         layer.loading(false);
                //         // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1+'^'+res.info;
                //         // // if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        
                //         // // if (id == 3) self.form.card_img3 = res.info;
                //         // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2+'^'+res.info;
                //         switch(id){
                //             case 1:
                //             self.img1 = res.info;
                //             self.form.allcard_img1 = res.info;
                //             break;
                //             case 2:
                //             self.img2 = res.info;
                //             self.form.allcard_img2 = self.img2;
                //             break;
                //             case 3:
                //             self.img3 = res.info;
                //             self.form.allcard_img1 = self.img1 +'^'+self.img3;
                //             break;
                //             case 4:
                //             self.img4 = res.info;
                //             self.form.allcard_img2 = self.img2 +'^'+self.img4;
                //             break;
                //             case 5:
                //             self.img5 = res.info;
                //             self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                //             break;
                //         }
                //     }, function () {//请求错误
                //         layer.open({
                //             content: '服务器响应错误'
                //             ,skin: 'msg'
                //             ,time: 1 //2秒后自动关闭
                //         });
                //         return;
                //     })
                // };
               
                
            },
            zoom (id) {
                var that = this
                var zoom ='';
                if (id == 1) zoom = this.imgstr.first
                if (id == 2) zoom = this.imgstr.second;
                if (id == 3) zoom = this.imgstr.first1;
                if (id == 4) zoom = this.imgstr.third;
                if (id == 5) zoom = this.imgstr.four;
                // console.log(zoom);
                layer.open({
                    type: 1,
                    content: '<img src="'+zoom+'" style="width:8rem";height:7rem;position:fixed; left:0;right:0;bottom:0;top:0;margin:auto;>',
                    anim: 'false',
                    style: ' border:none;',
                    success: function(elem){
                        that.forbidScroll()
                    },
                    end: function () {
                        that.startScroll()
                    }
              });
            },
            closeCity (val){//关闭城市弹出框
                this.cityFlag = false;
                this.form.card_city = val
                units.title.set('寻车定位');
            },
            getParm: function () {
                let cookdata = cookie.get('findCarForm');
                this.cards = cookie.get('cards') != null ? cookie.get('cards'):'';
                this.zl = cookie.get('zl') != null ? cookie.get('zl'):''
                if (cookdata) this.form = JSON.parse(cookdata);
                new Promise(() => {
                    let par = this.$route.query;
                    if (par.c) this.form.card_city = par.c;
                    if (par.m) this.form.card_model = par.m;
                    if (par.b) {
                        this.form.card_brand = par.b;
                        this.card.card_brand = par.id;
                        cookie.set('card_brand_id',par.id);
                        this.form.card_model = '';
                    }
                })
            },
            getCar:function () {
                let that = this;
                this.$http.post(units.host('car','Toolure'), units.params()).then(function (res) {
                    that.cardata = res.data;
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            brand () { //车辆品牌
                // this.$store.state.title = '车辆品牌';
                this.infoFlag = true
                
            },
            modelFn () {
                this.infoFlag = true
            },
            contract () {//签署电子合
                if(cookie.get('c_status') == '1'){//判断是否已经签署合同
                    this.$router.push('contracted')
                }else {
                    this.$router.push('contract')
                }
            },
            carBrand (url) { //车辆品牌
                this.forbidScroll();
                this.infoFlag = true;
                layer.loading('努力加载中,不要心急哦');
                this.getData(url)
                units.title.set('品牌选择');
            },
            getData (url) { //获取车辆品牌数据
            
                this.$http.post(units.host('brandtest', 'api'), units.paramsno()).then( function (res) {
                     if (res.ok) {
                        this.brandList = res.body;
                        layer.loading(false);
                        // console.log(res,1111)
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
            card_contract () {  //寻车期限
                this.timeFlag = true
                this.forbidScroll()
                // this.$refs.mark.style.overflow="hidden";
            },
            onValuesChange(picker, values) {//寻车期限（mint-ui）
                // console.log(picker, values)
                this.form.card_contract = values[0]
                // if (values[0] > values[1]) {
                //     picker.setSlotValue(1, values[0]);
                // }
            },
            cancelTime (val) { //寻车期限滑块取消按钮
                if(val == 0) {
                    this.form.card_contract = ''
                }
                this.startScroll()
                this.timeFlag = false
            },
            forbidScroll () {
                document.getElementsByTagName("html")[0].style.overflow="hidden";
                // document.getElementsByTagName("html")[0].style.height="100%";
                document.getElementsByTagName("body")[0].style.overflow="hidden";
                // document.getElementsByTagName("body")[0].style.height="100%"
            },
            startScroll () {
                document.getElementsByTagName("html")[0].style.overflow="visible";
                // document.getElementsByTagName("html")[0].style.height="auto";
                document.getElementsByTagName("body")[0].style.overflow="visible";
                // document.getElementsByTagName("body")[0].style.height="auto";
            },
            // sureTime () { //寻车期限滑块确定按钮
            //     this.timeFlag = false
            // },
            gpsFn () { //选择gps
                this.gpsFlag = true
            },
            closePicker (obj) {//关闭GPS
                if( obj.id == 0 ){ //取消
                    this.form.gps = '';
                    this.gpsShow = false;
                }else{ //确定
                    if(obj.gps == '是'){
                        this.gpsShow = true;
                        this.form.gps = 2;
                    }else{
                        this.gpsShow = false;
                        this.form.gps = 1;
                    }
                    this.gpsVal = obj.gps
                }
                this.gpsFlag = false
            },
            closeBrand (val) { //关闭车辆品牌弹出框
                this.startScroll();
                this.form.card_brand = val.cxname;
                this.car_ass_id = val.id
                units.title.set('寻车定位');
                this.infoFlag = false
            },
            brand () { //车辆品牌
                // this.$store.state.title = '车辆品牌';
                this.infoFlag = true
                
            },
            reexamination(find_id){//重新审核数据
            let that = this,
                host = units.getHost();
                this.$http.post(units.host('findcarSave'), units.paramsno({
                    find_id,
                })).then(function (res) {
                    if(!res.body.warning) {
                        if(res.body.code > 0) {
                            console.log(res.body.info);
                            that.reFindCarData = res.body.info; //获取所有信息
                            that.fail_reason = JSON.parse(that.reFindCarData.fail_reason); //将错误信息转为中文
                            
                            //错误审核时返回的信息
                            that.form.card_brand = res.body.info.card_brand;
                            that.form.card_number = res.body.info.card_number.slice(0,1);
                            that.form.card_allnumber = res.body.info.card_number.slice(1);
                            that.form.card_color = res.body.info.card_color;
                            that.form.allcard_img1 = res.body.info.card_img1;
                            that.form.allcard_img2 = res.body.info.card_img2;

                            let licenseCar = res.body.info.card_img1.split('^');
                            let ContractImg = res.body.info.card_img2.split('^');

                            if(licenseCar[0]) {
                                that.imgstr.first = host+licenseCar[0];
                                that.card_img1 = 'img1'
                            }
                            if(licenseCar[1]){
                                that.imgstr.first1 = host+licenseCar[1];
                                that.card_img2 = 'img2'
                            }
                            
                            if(ContractImg[0]){
                                that.imgstr.second = host+ContractImg[0];
                                that.card_img3 = 'img3'
                            }
                            if(ContractImg[1]){
                                that.imgstr.third = host+ContractImg[1];
                                that.card_img4 = 'img4'
                            }
                            if(ContractImg[2]){
                                that.imgstr.four = host+ContractImg[2];
                                that.card_img5 = 'img5'
                            }

                        } else{
                            layer.msg(res.body.msg)
                        }
                    } else {
                        layer.msg(res.body.warning)
                    }
                });
            }
        },
        beforeRouteLeave (to, from, next) {
            // console.log(this.$refs.detailInfo)
            if( this.infoFlag || this.cityFlag) {
                this.infoFlag = false
                this.cityFlag = false
                next(from.path)
                units.title.set('寻车定位');
                this.startScroll();//5.14
            } else {
                next()
            }
        },
        created: function () {
            let that = this;
            //1 车辆看护,2 寻车服务
            this.getParm();
            cookie.set('serviceType', 2);
            units.title.set('寻车定位');
            // this.cardtypes();
            this.getCar();
            if (cookie.get('c_status')  == 1) {//签合同 
                this.contractFlag = false
            }
            if(this.$route.query.zl) {
                this.zl = this.$route.query.zl;
            }  

            //判断是否是重新审核
            if(that.$route.query.find_id){
                let find_id = that.$route.query.find_id;
                this.reexamination(find_id);
            }
            this.$store.state.header.left = function () {
                that.startScroll();
                if(that.$route.query.type == '1') { //是否从重新审核通过
                    location.href = '#/server/content?cur=1';
                } else {
                    location.href = '#/';
                }
            }
            that.startScroll(); //5.11
            
        },
        mounted() {
            // if (cookie.get('c_status')  == 0){
            // let data = JSON.parse(cookie.get('findCarForm'));
        // }
        },
        beforeCreate: function () {
        //    console.log('beforeCreate')
        },
        beforeRouteEnter: function (to, from, next) {
            if(from.name == 'index' || from.name == 'orderList'){
                cookie.del('findCarForm');
                cookie.del('cards');
                cookie.del('zl');
                cookie.del('card_brand_id');
            }
            units.isLogin(true);
            next();
        },
        components: {
            listInfo,
            GpsPicker,
            City
        }
    }

</script>

<!--页面css样式-->
<style scoped lang='scss'>
    @import "../../static/mobiscroll/css/mobiscroll.jquery.min.css";
.select-dom{
    line-height: .7rem;
    border: .01rem solid #4c91ff;
    width:1.5rem;
    height:.7rem;
    color:#4c91ff;
    padding-left:.25rem;
    font-size: .45rem;
}
 /* --ie清除--*/

select::-ms-expand{ display: none; }

/* --火狐、谷歌清除--*/

select{
     appearance:none;  
    -moz-appearance:none;  
    -webkit-appearance:none;
     background: url("../assets/img/select.png") no-repeat scroll  transparent;
     background-size: .3rem;
     background-position: 80% 50%;
     padding-right: .4rem;
}
/* --箭头就用自己设计的箭头，padding 空出箭头的位置--*/
    .explain-text{
        font-size: .35rem;
        line-height: .5rem;
        color: red;
        margin-top: .5rem; 
        font-family: 'Courier New', Courier, monospace;
    }
    // 机动车登记图片
    .license-ul1{
        display: flex;
        justify-content: space-between;
        .li{
            width: 3.1rem;
            .img-box{
                position: relative;
                width: 3.1rem;
                height: 3.1rem;
                background: url(../assets/img/img_13.jpg);
                .img-mark{ //图片的遮罩
                    position: absolute;
                    top: 0;
                    left: 0;
                    right: 0;
                    bottom: 0;
                    background: rgba(0, 0, 0, .5);
                    width: 3.1rem;
                    height: 3.1rem;
                }
            }
            img{
                width: 3.1rem;
                height: 3.1rem;
            }
            .upload-btn{
                width: 3.1rem;
                height: 1rem;
                background: url(../assets/img/upload-btn2.png) center;
                // background: #4c91ff;
                background-size:cover; 
                text-align: center;
                color: #fff;
                font-size: .4rem;
                line-height: 1rem;
                input{
                    width: 100%;
                    opacity: 0;
                    font-size: .62rem;
                }
            }
        }
    }
    // gps内容
    .gps-page{
        margin-top: .25rem;
    }
    // 寻车期限
    .card-time-mark{
        position: fixed;
        top:0;
        left:0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .5);
        z-index: 1000;
    }
    .card_contract-box{
        background: #fff;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        padding-bottom: .5rem;
        .btn-box{
            display: flex;
            justify-content: space-between;
            background: #eaeaea;
            button{
                width: 2rem;
                height: 1rem;
                font-size: .5rem;
                margin: 0 .5rem;
                border: 0;
                background: #eaeaea;
            }
        }
    }
    .license-title{
        font-size: .48rem; 
        padding-bottom:.4rem; 
    }
    #Findcar{
        padding-top:$top; //头部paddingTop
        background: #f0f0f0;
    }
    .resg {
        background: #f0f4fa;
        font-size: 0.36rem;
        line-height: 0.6rem;
        padding: 0.52rem 0.38rem;
        color: #787878;
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }

    .in_list li {
        height: 1.49rem;
        overflow: hidden;
        padding:0 0.4rem;
        box-sizing: border-box;
    }

    .in_list li a {
        display: block;
        position: relative;
        height: 1.49rem;
        line-height: 1.49rem;
        min-height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
    }

    .in_list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
        position: relative;
        top: -.07rem;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 76%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
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
        background: url(../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a .arrow_right_only {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
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
    .arrow_right_text{
        float: right;
        color: #2c7dfe;
        font-size: .4rem;
    }
    .pledge {
        margin-top: 0.3rem;
        background: #fff;
        padding: 0.4rem;
    }

    .picture {
        border: 1px dashed #bcc6d6;
        margin-bottom: 0.3rem;
        text-align: center;
        position: relative;
        background-size: 50%;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;
        padding-bottom:.3rem; 
        padding-right:.3rem; 
        img{
            width:2.1rem;
            height: 2.1rem;
            text-align: center;
            position: relative;
            top: .3rem;
            left: .3rem;        
        }
        .thumb1{
            margin-left:2rem;
            border:2px red solid;  
        }
        div{
            background: url(../../src/assets/img/license_bg.png) no-repeat center;
            background-size: 100%;
            width: 2.1rem;
            height: 2.1rem;
            margin-top: .3rem;
            margin-left:.3rem; 
            input{
                width:100%;
                height: 100%;
            }
            .file{
                width:100%;
                height: 100%;
                font-size: .01rem;
                opacity: 0;
            }
        }
        
    }

    .borrow {
        border: 1px dashed #bcc6d6;
        margin-bottom: 0.3rem;
        text-align: center;
        position: relative;
        background-size: 20%;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;
        padding-bottom:.3rem; 
        padding-right:.3rem;
        div{
            background: url(../../src/assets/img/license_bg.png) no-repeat center;
            background-size: 100%;
            width: 2.1rem;
            height: 2.1rem;
            margin-top: .3rem;
            margin-left:.3rem; 
            input{
                width:100%;
                height: 100%;
            }
            .bow_file{
                width:100%;
                height: 100%;
                font-size: .01rem;
                opacity: 0;
            }
        }
    }

    .picture img {
        // width: 100%;
        /*height: 3rem;*/
        text-align: center;
        position: absolute;
        /*width: 1.88rem;*/
        /*height: 1.23rem;*/
        /*text-align: center;*/
        /*position: absolute;*/
        /*top: 31%;*/
        /*left: 40%;*/
    }

    .borrow img {
        width: 2.1rem;
        height: 2.1rem;
        text-align: center;
        position: absolute;
        top:0.3rem;
        left:0.3rem;
    }

    .aptitude {
        color: #787878;
        font-size: 0.3rem;
        line-height: 0.48rem;
        margin-top: 0.5rem;
    }

    .pact {
        color: #F05C27;
        font-size: 0.3rem;
        margin-top: 0.24rem;
    }

    .fixed-ad-layer {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 1000;
        background: rgba(0, 0, 0, .8);
        -webkit-transform: translate3D(0, 0, 0);
        transform: translate3D(0, 0, 0);
    }

    .fixed-ad-layer .fixed-ad-con {
        width: 300px;
        margin: 0 auto;
        position: absolute;
        left: 50%;
        top: 50% !important;
        -webkit-transform: translateY(-50%);
        transform: translateY(-50%);
        margin-left: -150px;
    }

    .fixed-ad-layer .fixed-ad-con .fixed-ad-img {
        display: block;
        text-align: center;
        max-width: 300px;
        height: auto;
        position: relative;
    }

    .fixed-ad-layer .fixed-ad-con .fixed-ad-img img {
        max-width: 100%;
        height: auto;
    }

    .close-fixed-ad {
        position: relative;
        width: 14px;
        height: 14px;
        bottom: 0px;
        z-index: 2;
        background: url(../../src/assets/img/xxxx.png);
        background-size: cover;
        left: 50%;
        margin-left: -18px;
        margin-top: 30%;
        cursor: pointer;
    }

    .p1 {
        position: absolute;
        top: 48%;
        color: #fff;
        font-size: 0.7rem;
        left: 37%;
    }

    .p2 {
        position: absolute;
        color: #787878;
        bottom: 0.9rem;
        font-size: 0.38rem;
        line-height: 0.8rem;
        padding: 0 0.9rem;
    }
   
</style>