<template>
    <div class="information-details">
        <div class="info-details-title">{{singleData.title}}</div>
        <div class="main-info">
            <span class="info-img" v-if='singleData.content'>
                <img v-if='singleData.user_header' :src="units.getHost()+singleData.user_header">
                <img v-else src="../../assets/img/header-img.png" >
                <span class="info-name" v-if='singleData.uid != uid'>{{singleData.user_mobile.slice(0,3)}}****{{singleData.user_mobile.slice(7)}}</span>
                <span class="info-name" v-else>{{singleData.user_mobile}}</span>
            </span>
            <span></span>
        </div>
        <div class="info-time-box">
            <span>{{new Date(singleData.release_time*1).getFullYear()}}-{{new Date(singleData.release_time*1).getMonth()+1}}-{{new Date(singleData.release_time*1).getDate() }} &nbsp;&nbsp;{{new Date(singleData.release_time*1).getHours() }}:{{new Date(singleData.release_time*1).getMinutes() }}</span>
            <b>·</b>
            <span>阅读<span>{{singleData.read_num}}</span></span>
        </div>
        <div class="info-content-box">
            {{singleData.content}} 
        </div>
    </div>
</template>

<script>
import units from '@/tools/units'
import cookie from '@/tools/cookie'
export default {
    data () {
        return {
            singleData: {},
            uid: ''
        }
    },
    created () {
        let that = this;
        units.title.set('详情');
        this.uid = cookie.get('user_id')
        this.$store.state.header.right = false;
        let id = JSON.parse(this.$route.query.id);
        // this.$http.post(units.host('get_content_readnum','api'),{ //计算阅读数
        //     id
        // }).then(function (res) {
        //         // console.log(res)
        // })
        // 请求详情数据
        // layer.msg('请求中...')
        this.$http.post(units.host('get_content_detail','api'), units.paramsno({
            id
        })).then(function (res) {
            if (!res.body.warning) {//
                if (res.body.code > 0) {
                    that.singleData = res.body.info[0];
                } else {
                    layer.msg(res.body.code);
                }
            }else {
                layer.msg(res.body.warning)
            }
        }, function () {//请求错误
            layer.open({
                content: '服务器响应错误'
                ,skin: 'msg'
                ,time: 1 //2秒后自动关闭
            });
            return;
        })
        this.$store.state.header.left = function () {
           that.$router.go(-1)
        };
    } 
}
</script>

<style lang='scss' scoped>
    .information-details{
        padding: $top .5rem;
        background: #fff;
        height: 100%;
        overflow-x: hidden;
        .info-details-title{
            font-weight: 600;
            font-size: .65rem;
            padding-top:.6rem; 
        }
        .main-info{
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: .3rem 0 .2rem 0;
            .info-img{
                img{
                    width: 1.2rem;
                    height: 1.2rem;
                    border-radius: 50%;
                }
                .info-name{
                    position: relative;
                    top: -.05rem;
                    font-size: .42rem;
                }
            }
        }
        .info-time-box{
            padding:  .2rem 0 .5rem;
            color: #bebebe;
            font-size: .4rem;
            b{
                padding: 0 .3rem;
            }
        }
        .info-content-box{
            font-size: .5rem;
            line-height: 1rem;
            box-sizing: border-box;
        }
    }
</style>
