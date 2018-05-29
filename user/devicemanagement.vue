<template>
<!--  -->
    <div class="device-management-box" v-if='machineList.statistics_machine' >
        <div class="device-nav">
            <span @click="shotTab(0)" :class='{"curActive": curActiveFlag == 0}'><span class="text">识别拍摄数量</span></span>
            <span @click="shotTab(1)" :class='{"curActive": curActiveFlag ==1}'><span class="text">报警车辆拍摄数</span></span>
        </div>
        <div class="device-content-box">
            <div class='device-content-page' v-show="currentID == 0">
                <div class="device-title"><b>识别拍摄数量</b></div>
                <ul class="device-content">
                    <li class="device-content-li">
                        <span>当天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.today_num?machineList.statistics_machine.today_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近7天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.week_num?machineList.statistics_machine.week_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近30天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.month_num?machineList.statistics_machine.month_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>识别总数量</span>
                        <span class="blue-color">{{machineList.statistics_machine.total_num?machineList.statistics_machine.total_num:0}}</span>
                    </li>
                </ul>
            </div>  
            <div class='device-content-page' v-show='currentID == 1'>
                <div class="device-title"><b>报警车辆拍摄数</b></div>
                <ul class="device-content">
                    <li class="device-content-li">
                        <span>当天报警数</span>
                        <span class="blue-color">{{machineList.statistics_machine.today_find_num?machineList.statistics_machine.today_find_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近7天报警数</span>
                        <span class="blue-color">{{machineList.statistics_machine.week_find_num?machineList.statistics_machine.week_find_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近30天报警数</span>
                        <span class="blue-color">{{machineList.statistics_machine.month_find_num?machineList.statistics_machine.month_find_num:0}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>报警总数量</span>
                        <span class="blue-color">{{machineList.statistics_machine.total_find_num?machineList.statistics_machine.total_find_num:0}}</span>
                    </li>
                </ul>
            </div>  
        </div>

        <div class="photographing-num">
            <div><b>拍摄机共有{{machineList.machine_num?machineList.machine_num:0}}台</b></div>
        </div>
        <div class="photographing-list-box">
            <div class="photographing-title">拍摄机列表</div>
            <div class="photographing-list">
                <div 
                    class="photographing-li"
                    v-for='(val, ind) in machineList.machine_list'
                    :key='ind'
                    >
                    <span><b>{{val.account}}</b><small>（{{val.mark?val.mark:'易寻'}}）</small></span>
                    <span class="blue-color" @click="watchDetail(val.id)">查看</span>
                </div>
            </div>
        </div>

        <!-- 拍摄机详情弹出框 -->
        <div class="photographing-mark-box" v-if='closeShotFlag && machineDetails.data' @click.stop.prevent="closeShotAlert(machineDetails)">
            <div class="photographing-content" @click.stop>
                <div class="photographing-mark">
                    <div class="photographing-info">
                        <div class="user-name-box">
                            <div class="user-name" v-if='edit'>使用者名称：{{machineUser?machineUser:'易寻'}}</div>
                            <div class="user-name" v-else>使用者名称：<input type="text" v-model="reviseName"></div>
                            <div class="edit" @click="editFn"><span v-if='edit'>编辑</span><span v-else>完成</span></div>
                        </div>
                        <div class="photographing-name">
                            拍摄机名称：{{machineDetails.data.account}}
                        </div>
                    </div>
                    <div class="shot-sum">
                        <div class="shot-sum-title"><b>拍摄总数</b></div>
                        <div class="shot-sum-box">
                            <div class="shot-sum-li">
                                <span>当天拍摄数</span>
                                <span class="grey-color">{{machineDetails.car_data.today_num?machineDetails.car_data.today_num:0}}</span>
                            </div>
                            <div class="shot-sum-li">
                                <span>近7天拍摄数</span>
                                <span class="grey-color">{{machineDetails.car_data.week_num?machineDetails.car_data.week_num:0}}</span>
                            </div>
                            <div class="shot-sum-li">
                                <span>近30天拍摄数</span>
                                <span class="grey-color">{{machineDetails.car_data.month_num?machineDetails.car_data.month_num:0}}</span>
                            </div>
                            <div class="shot-sum-li">
                                <span>识别总数量</span>
                                <span class="grey-color">{{machineDetails.car_data.total_num?machineDetails.car_data.total_num:0}}</span>
                            </div>
                        </div>
                    </div>
                    <div class="shot-sum">
                        <div class="shot-sum-title"><b>已报警总数</b></div>
                        <div class="shot-sum-box">
                            <div class="shot-sum-li">
                                <span>当天报警数</span>
                                <span class="grey-color">{{machineDetails.car_data.today_find_num? machineDetails.car_data.today_find_num:0}}</span>
                            </div>
                            <div class="shot-sum-li">
                                <span>近7天报警数</span>
                                <span class="grey-color">{{machineDetails.car_data.week_find_num?machineDetails.car_data.week_find_num:0}}</span>
                            </div>
                            <div class="shot-sum-li">
                                <span>近30天报警数</span>
                                <span class="grey-color">{{machineDetails.car_data.month_find_num?machineDetails.car_data.month_find_num:0}}</span>
                            </div>
                            
                            <div class="shot-sum-li">
                                <span>报警总数量</span>
                                <span class="grey-color">{{machineDetails.car_data.total_find_num?machineDetails.car_data.total_find_num:0}}</span>
                            </div>
                        </div>
                    </div>
                    <div class="close-btn"><button @click.stop="closeShotAlert(machineDetails)"></button></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import units from '../../tools/units'
import cookie from '@/tools/cookie'
export default {
    name: 'devicemanagement',
    data () {
        return {
            currentID: 0,
            curActiveFlag: 0,
            machineUser: '我是傻子',//使用者的备注
            closeShotFlag: false, //拍摄机详情弹出框
            edit: true, //判断是否处于编辑状态
            user_id: '',
            machineList: {}, //大区经理设备统计接口
            machineDetails: {}, //每个设备详情
            everyId: 0, //每个设备机的id
            reviseName: '', //修改后的名字
            scrollTop: 0,//滚动条距离顶部的距离
        }
    },
    methods: {
        shotTab (id) { //Tab切换
            this.currentID = id;
            this.curActiveFlag = id
        },
        watchDetail (id) { //查看每一台摄像机详情
            this.everyId = id;
            this.scrollTop = $(window).scrollTop();
            this.$http.post(units.domin('Hardware/machineInfo'), units.paramsno({ id })).then( function (res) {
                if (res.ok) {
                    // console.log(this.scrollTop,12)
                    // console.log($('html').scrollTop())
                    // console.log(document.documentElement.scrollTop)
                    console.log($(window).scrollTop())
                    // console.log($('body').scrollTop())
                    this.forbidScroll();
                    this.machineDetails = res.body.info;
                    this.machineUser = this.machineDetails.data.mark;
                    this.closeShotFlag = true;
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
        editFn () {//编辑备注
           if(this.edit) {
               this.edit = false
           } else {
               this.$http.post(units.domin('Machines/updateMachine'), units.paramsno({
                    id:this.everyId,
                    switch:'savemark',
                    mark: this.reviseName
                })).then( function (res) {
                    
                    if (res.ok) {
                        layer.msg(res.body.msg)
                        this.machineUser = this.reviseName
                        this.reviseName = ''
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
               this.edit = true
           }
        },
        closeShotAlert (detail) { //关闭拍摄机详情弹出框
            this.startScroll();
            this.closeShotFlag = false;
            this.getMachineData ()
        },
        getMachineData () { //大区经理设备统计接口数据
            this.$http.post(units.domin('Machines/statisticsMachine'), units.paramsno({
                role:1,
                uid:this.user_id,
            })).then( function (res) {
                if(res.body.code > 0) {
                    if (res.ok) {
                        this.machineList = res.body.info
                    }
                } else {
                     layer.open({
                        content: res.body.msg
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
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
        forbidScroll () {
            document.getElementsByTagName("html")[0].style.overflow="hidden";
            document.getElementsByTagName("html")[0].style.height="100%";
            document.getElementsByTagName("body")[0].style.overflow="hidden";
            document.getElementsByTagName("body")[0].style.height="100%"
        },
        startScroll () {
            document.getElementsByTagName("html")[0].style.overflow="visible";
            // document.getElementsByTagName("html")[0].style.height="auto";
            document.getElementsByTagName("body")[0].style.overflow="visible";
            // document.getElementsByTagName("body")[0].style.height="auto";
            // $('html').scrollTop(this.scrollTop);
            $(window).scrollTop(this.scrollTop)
            
        },
    },
    created () {
        units.title.set('设备详情');
        this.user_id = cookie.get('user_id')
        this.getMachineData ();
    }
}
</script>

<style scoped lang='scss'>
    .blue-color{
        color: #3d87ff;
        font-weight: bolder;
        vertical-align: bottom;
    }
    .grey-color{
        color: #787878;
        vertical-align: bottom;
    }
    .device-management-box{
        padding-top: $top;
        padding-bottom: 1.5rem; 
        font-size: .45rem;
        .device-nav{ //导航
            display: flex;
            background: #fff;
            span{
                flex:1;
                border: .01rem solid #f2f6f7;
                text-align: center;
                &:nth-child(1){
                    border:0;
                }
                &.curActive span{
                    border-bottom: .06rem solid #3d7fed;
                }
                .text{
                    display: inline-block;
                    padding: .2rem 0;
                    border-bottom: .06rem solid #fff;
                }
            }
        }
        .device-content-box{  //拍摄/报警的详细内容
            margin-top: .35rem;
            .device-title{
                line-height: 1.3rem;
                padding: 0  .5rem; 
                box-sizing: border-box;
                font-size: .5rem;
            }
            .device-content{
                background: #fff;
                width: 100%;
                padding-bottom: .7rem; 
                li{
                    padding: 0  .5rem; 
                    padding-top: .7rem; 
                    box-sizing: border-box;
                    display: flex;
                    justify-content: space-between;
                }
            }
        }
        .photographing-num{ //拍摄机总数
            line-height: 2rem;
            text-align: center;
            color: #ff671c;
            background: #fff;
            padding: 0  .5rem;
            box-sizing: border-box;
            div{
                border-top: .01rem solid #eeeeee;
                font-size: .5rem;
            }
        }
        .photographing-list-box{ //拍摄机列表
            margin-top: .35rem;
            .photographing-title{
                line-height: 1.3rem;
                padding: 0  .5rem; 
                box-sizing: border-box;
                font-size: .5rem;
            }
            .photographing-list{
                background: #fff;
                .photographing-li{
                    display: flex;
                    justify-content: space-between;
                    margin: 0 .5rem;
                    padding: .4rem 0;
                    border-bottom: .01rem solid #eeeeee;
                }
            }
        }
        .photographing-mark-box{//拍摄机详情弹出框
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0, 0.5);
            z-index: 999;
            .photographing-mark{
                width: 8.5rem;
                height: 12rem;
                overflow-y: scroll;
                overflow-x:hidden; 
                box-sizing: border-box;
            }
            .photographing-content{
                // margin: 10% 0 0 50%;
                position: absolute;
                top: 20%;
                left: 50%;
                right: 0;
                width: 8.5rem;
                transform: translate(-50%);
                background: #fff;
                border-radius: .1rem;
                .photographing-info{
                    box-sizing: border-box;
                    padding:  0 .6rem;
                    .user-name-box{
                        display: flex;
                        justify-content: space-between;
                        padding-top: .6rem; 
                        .user-name{
                            input{
                                border:.01rem solid #ccc;
                                width: 2.2rem;
                                height: .6rem;;
                            }
                        }
                    }
                    .edit{
                        color: #ff671c;
                    }
                    .photographing-name{
                        padding:  .35rem 0;
                    }

                }
                .shot-sum{//拍摄机总数
                    .shot-sum-title{
                        width: 99.6%;
                        padding: .4rem .6rem .1rem .6rem;
                        box-sizing: border-box;
                        line-height: 1rem;
                        background: #f0f4fa;
                    }
                    .shot-sum-box{
                        box-sizing: border-box;
                        padding:0 .6rem;
                        .shot-sum-li{
                            padding-top: .5rem;
                            display: flex;
                            justify-content: space-between;
                            &:last-child{
                                padding-bottom: .5rem;
                            }
                        }
                    }
                }
            }
            .close-btn{
                width: 99.6%;
                // height: 1.9rem;
                text-align: center;
                background: #f0f4fa;
                border-radius: .1rem;
                padding: .5rem 0;
                button{   
                    
                    width: 7.3rem;
                    height:1.3rem;
                    border: 0;
                    outline: none;
                    background: url(../../assets/img/close-btn.png) no-repeat center;
                    background-size: 100%;
                }
            }
        }
    }
</style>
