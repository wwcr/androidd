<template>
    <div class="series-page-box" ref='seriesBox'>
        <div class="series-title">车系<span class="closeBtn" @click="closeModel(0)">×</span></div>
        <div class="wrapper" ref='wrapper'>
            <div class="content">
                <ul class="series-content">
                    <li
                        v-for='(val,ind) in seriesList'
                        :key='ind'
                        @click='checkModel(val)'
                    >
                        <span>{{val.xlname}}</span>
                        <label for=""></label>
                    </li>
                </ul>
            </div>
        </div>
        <modelList 
            v-show='modelFlag'
            @closeModel='closeModel'
            :modelList = 'modelList'/>
    </div>
</template>
<script>
import Bscroll from 'better-scroll'
import units from '../../tools/units'
import modelList from '@/components/frame/modelList'
export default {
    name:'series',
    props: ['seriesList'],
    data () {
        return {
            modelFlag: false,
            modelList: []
        }
    },
    methods: {
        checkModel (val) {
            this.getModel(val.xlid)
            this.modelFlag = true
            // this.$emit('closeseries',{series: series, ind: ind})
        },
        getModel (id){//获取车系
            this.$http.post(units.host('car_list','api'), units.paramsno({id})).then( function (res) {
                if (res.ok) {
                    this.modelList = res.body
                    // console.log(res)
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
        closeModel (val) {
            if(val != 1) { 
                this.$emit('closeSeries', val)
            }
            this.modelFlag = false
        }
    },
    // updated () {
    //     this.$nextTick(() => {
    //         this.scroll = new Bscroll(this.$refs.wrapper, {
    //             scrollY: true,
    //             scrollbar: true,
    //             click: true
    //         })
    //     })
    // },
    created () {
        // this.$nextTick(() => {
        //     this.scroll = new Bscroll(this.$refs.wrapper, {
        //         scrollY: true,
        //         scrollbar: true,
        //         click: true
        //     })
        // })
    },
    components: {
        modelList
    }
}
</script>
<style scoped lang='scss'>
    .box-width{
        width: 70%;
    }
    
    .series-page-box{
        // padding-top: 1.5rem;
        border-left:.2rem solid  #f0f4fa;
        font-size: .5rem;
        width: 70%;
        position: fixed;
        background: #fff;
        right:0;
        top:$top;
        bottom: 0;
        font-size:.45rem;
        .series-title{
            padding:.2rem .4rem;
            background: #f0f4fa;
            font-size: .4rem;
            position: relative;
            width: 100%;
            .closeBtn{
                position: absolute;
                top:.1rem;
                right: .5rem;
                font-size: .7rem;
            }
        }
        .wrapper {
            width: 100%;
            background: #fff;
            overflow-y: scroll;
            position: absolute;
            top: 1rem;
            bottom: 0;
            // height: 100%;
            z-index: 99;
            .content {
                position: relative;
                padding: 0 10px;
                top: 0;
                left: 0;
                right: 0;
            }
        }
        .series-content{
            background: #fff;
            li{
                border-bottom: .01rem solid #f0f0f0; 
                line-height: 1.2rem;
            }
        }
    }
</style>
