<template>
    <div class="information-box"
        v-infinite-scroll="loadMore"
        infinite-scroll-disabled="loading"
        infinite-scroll-distance="1"
        infinite-scroll-immediate-check=false    
    >
    <mt-loadmore 
                :top-method="loadTop" 
                @top-status-change="handleTopChange"
                ref="loadmore">
                <div slot="top" class="mint-loadmore-top">
                    <!-- 下拉刷新状态提示语 -->
                    <span v-show="topStatus == 'drop'" style="font-size: .3rem;">释放立即刷新</span>
                    <span v-show="topStatus == 'loading'" ><img class="loading-img" src="../../assets/img/loading.gif" alt=""></span>
                    <span v-show="topStatus == 'pull'" style="font-size: .3rem;">下拉刷新</span>
                </div>
         <!-- <v-scroll  :on-refresh="onRefresh" :on-infinite="onInfinite" :dataList="scrollData"> -->
            <div class="information-list">
                <div 
                    class="information-div" 
                    v-for = "(val,ind) in informationList"
                    :key='ind'
                    >
                    <div class="main-info">
                        <div class="info-img">
                            <div class="head-img"><img 
                                v-if='val.user_header'
                                :src="units.getHost()+val.user_header"
                                @click='allinfolist(val.uid)'
                            >
                            <img 
                                v-else
                                src="../../assets/img/header-img.png"
                                @click='allinfolist(val.uid)'
                            >
                            </div>
                            <div class="info-name" v-if='val.uid != uid'>{{val.user_mobile.slice(0,3)}}****{{val.user_mobile.slice(7)}}</div>
                            <div class="info-name" v-else>{{val.user_mobile}}</div>
                        </div>
                        <!-- 时间 -->
                        <span class="info-time" v-if='(new Date()*1 - val.release_time)/1000 < 60'>刚刚</span>
                        <span class="info-time" v-if='(new Date()*1 - val.release_time)/1000 < 3600  && (new Date()*1 - val.release_time)/1000 > 60'>{{parseInt((new Date()*1 - val.release_time)/1000/60)}}分钟前</span>
                        <span class="info-time" v-else-if ='(new Date()*1 - val.release_time)/1000/3600<24 && (new Date()*1 - val.release_time)/1000/3600>1'>{{parseInt((new Date()*1 - val.release_time)/1000/3600)}}个小时前</span>
                        <span class="info-time" v-else-if='(new Date()*1 - val.release_time)/1000/3600>24'>{{new Date(val.release_time*1).getFullYear()}}年{{new Date(val.release_time*1).getMonth()+1}}月{{new Date(val.release_time*1).getDate()}}日</span>

                        <!-- 时间结束 -->
                    </div>
                    <div class="info-title" v-if='val.title'>{{val.title}}</div>
                    <div class="info-content-box">
                        <div class="info-content">
                            <!-- <span class="location">北京朝阳区</span> -->
                            <span class="detail-content">{{val.content}}</span>
                        </div>
                        <div class="info-btn" @click="details(val.id)">详情</div>
                    </div>
                </div>
            </div>
            <div class="loading-icon" style="font-size:.35rem;" v-show='icon'><img src="../../assets/img/loading.gif" alt=""></div>
            <div class="loading-icon" v-show='allLoaded' style="font-size:.35rem;">暂无更多数据</div>
        </mt-loadmore>
        <div class="warning-box" v-if='!informationList'>暂无任何消息</div>
        <!-- </v-scroll> -->
    </div>
</template>

<script>
import units from '@/tools/units'
import cookie from '@/tools/cookie'
export default {
    data () {
        return {
            informationList: [],// 下拉更新数据存放数组
            uid: '',
             page:1,
            articlePage: 0,
            articleLimit: 8,
            allarticle:'',
            loading:'',
            icon:false,
            complete: false, //数据是否显示完成
            distance:0,
            allLoaded:false,
            topStatus: '',
        }
    },
    methods: {
        loadTop() {//下拉刷新
            setTimeout(() => {
                this.getlist(2);
                this.$refs.loadmore.onTopLoaded();
            }, 500);//延时执行
            // 可以加上刷新完成
        },
        handleTopChange(status) { //下拉刷新状态
            setTimeout(() => {
            }, 500);//延时执行
            this.topStatus = status;
        },
        loadMore(){ //无限加载
        // console.log(11111)
            this.icon = true;
            setTimeout(() => {
                this.getlist(1);
            }, 500);//延时执行
        },
        details (val) { //单个数据详情页
        // console.log(JSON.stringify(val));
            location.href = '#/informationdetails?id='+val + '&msg='+ 1;
        },
        allinfolist (uid) {//本账号发表的数据
            location.href = '#/homepage?id=' + uid
        },
        // onRefresh (done) { //下拉上拉...
        //     this.getlist(2);
        //     // this.getArticle(this.currentNum,1);
        //     done(); // call done

        // },
        // onInfinite(done) {//下拉上拉...
        //     this.getlist(3);
        //     this.counter++;
        //     let end = this.pageEnd = this.num * this.counter;
        //     let i = this.pageStart = this.pageEnd - this.num;
        //     // console.log()
        //     let more = this.$el.querySelector('.load-more-main');
        //     console.log(more);
        //     for(i; i < end; i++) {
        //         if(i >= 30) {
        //             more.style.display = 'none'; //隐藏加载条
        //             //走完数据调用方法
        //             this.scrollData.noFlag = true;
        //             break;
        //         } else {
        //             this.listdata.push({
        //                 date: "2017-06-1"+i,
        //                 portfolio: "1.5195"+i,
        //                 drop: i+"+.00 %" ,
        //                 state: 2
        //             })
        //             more.style.display = 'none'; //隐藏加载条
        //                 // console.log(111);
        //         }
        //     }
        //     done();
        // },
         getlist:function (id) {
                let that = this;
                if(id == 1){//如果是上拉加载
                    that.articlePage = that.articlePage + that.articleLimit;
                    if((that.articlePage + that.articleLimit) > that.allarticle){
                        this.icon = false;
                        this.loading= true;// 若数据已全部获取完毕
                        this.allLoaded = this.loading;
                    }
                }
                if(id == 2){
                    that.articlePage = 0;
                }
                this.$http.post(units.host('get_all_contentlist','api'), units.paramsno({
                        limit:that.articleLimit+that.articlePage,
                        page:that.page++,
                    })).then(function (res) {
                        if (!res.body.warning) {//
                            if (res.body.code > 0) {
                                that.informationList = res.body.info;
                                // console.log(res)
                                that.allarticle = res.body.msg;//总条数
                                if(id == 2){//下拉刷新
                                    that.loading = false;
                                }
                                if(id == 3){
                                    that.loading = false;//刚刷新进入 不让执行
                                }
                            } else {
                                layer.msg(res.body.code);
                            }
                        }else {
                            layer.msg(res.body.warning);
                            setTimeout(()=>{  //几秒之后返回上一页
                                window.history.go(-1);
                                return;
                            }, 1000)
                        }
                    }, function () {//请求错误
                        layer.open({
                            content: '服务器响应错误'
                            ,skin: 'msg'
                            ,time: 1 //2秒后自动关闭
                        });
                        setTimeout(()=>{  //几秒之后返回上一页
                            window.history.go(-1);
                            return;
                        }, 1000);
                    })
            }
    },
    components: {
        'v-scroll': require("../pull-refresh_message")
    },
    beforeDestroy () {
        this.$store.state.header.right = false;
    },
    created () {
        let that = this;
        units.title.set('业务资讯');
        this.uid = cookie.get('user_id')
        this.$store.state.header.right = true;
        this.$store.state.header.rightContent = '发表';

        this.$store.state.header.rightTouch = function () { //点击发表
            location.href = '#/publish'
        }
        this.$store.state.header.left = function () {
            that.$store.state.header.right = false;
            location.href = '#/';
            // window.history.back()
        };
        this.getlist(3);
    }
}
</script>
<style lang='scss' >
.warning-box{
    text-align: center;
    font-size: .4rem;
    margin-top: .5rem;
}
// 加载的loading样式
    .loading-icon{
        text-align: center;
        padding: .2rem 0 .4rem 0;
        img{
            width: .45rem;
            height: auto;
        }
    }
    .loading-img{
        width: .4rem;
        height: auto;
    }
// 加载的loading样式结束
// // 上拉加载
// .yo-scroll .inner .load-more-main{
//     margin-top: .1rem!important;
// }
// // 上拉加载结束
// </style>

// <style lang='scss' scoped>
// // 上拉加载
// .yo-scroll{
//     top: 1.7rem !important;
//     font-size: .42rem;
// }

.information-box{
    padding-top:$top + .5rem;
    // padding-bottom: 2rem;
    background: #f0f4fa;
    font-size:  .42rem;
    height: 100%;
    .information-list{
        background: #f0f4fa;
        box-sizing: border-box;
        .information-div{
            background: #fff;
            margin-bottom: .32rem;
            padding: 0 .4rem .35rem .4rem;
            .main-info{
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding: .3rem 0 .2rem 0;
                .info-img{
                    display: flex;
                    align-items: center;
                    .head-img{
                        width: 1.2rem;
                        height: 1.2rem;
                        border-radius: 50%;
                        img{
                            width: 100%;
                            height: 100%;
                            border-radius: 50%;
                        }
                    }
                    .info-name{
                        position: relative;
                        top: .1rem;
                        font-size: .42rem;
                        margin-left: .3rem;
                    }
                }
                .info-time{
                    color: #dcdcdc;
                    font-size: .35rem;
                }
            }
            .info-title{
                font-size: .48rem;
                font-weight: 600;
                width: 60%;
                height: 1.1rem;
                line-height: 1.1rem;
                overflow: hidden;
                text-overflow:ellipsis;
                white-space: nowrap;
            }
            .info-content-box{
                display: flex;
                justify-content: space-between;
                align-items: center;
                margin-top: .1rem;
                .info-content{
                    color: #dcdcdc;
                    width: 80%;
                    overflow: hidden;
                    text-overflow:ellipsis;
                    white-space: nowrap;
                }
                .info-btn{
                    color:#2c7dfe;
                }
            }
        }
    }
}
</style>
