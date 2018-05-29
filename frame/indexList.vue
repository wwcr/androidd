<template>
<!-- 寻车 车辆品牌 -->
    <div class="index-list-box">
        <!-- <div class="wrapper" ref='wrapper'>
            <div class="content"> -->
                <mt-index-list>
                     <template v-for='(val,index) in brandList'>
                         <mt-index-section
                            :key='index'
                            :index='index' 
                            >
                            <mt-cell 
                                v-for='(value) in val'
                                :title='value.big_ppname' 
                                :key='value.id'
                                @click.native="checkCar(value)">
                            <p ></p>
                            </mt-cell>
                        </mt-index-section>
                     </template>
                </mt-index-list>
                <seriesList 
                    v-show='seriesFlag'
                    @closeSeries = 'closeSeries'
                    :seriesList = 'seriesList'/>
           <!-- </div>
       </div>  -->
    </div>
</template>
<script>
    import Vue from 'vue';
    import units from '../../tools/units'
    import { IndexList, IndexSection  } from 'mint-ui';
    import Bscroll from 'better-scroll'
    import seriesList from '@/components/frame/seriesList'
    Vue.component(IndexList.name, IndexList);
    Vue.component(IndexSection.name, IndexSection);
    export default {
        name:'indexList',
        props: ['brandList'],
        data () {
            return {
                seriesFlag: false,//车系列表
                seriesList: []
            }
        },
        methods: {
            checkCar (val) {
                this.seriesFlag = true
                // console.log(val.id)
                this.getSeries(val.id)
                // this.$emit('closeCar', car)
            },
            getSeries (id){//获取车系
                this.$http.post(units.host('series','api'), units.paramsno({id})).then( function (res) {
                     if (res.ok) {
                        this.seriesList = res.body
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
            closeSeries (val) {
                if(val) {
                    this.$emit('closeBrand', val)
                }
                this.seriesFlag = false
            }
        },
        components: {
            seriesList
        }
    }
</script>
<style scoped lang='scss'>

     .index-list-box{
        background: #fff;
        width: 100%;
        position: fixed;
        top: $top;
        bottom: 0;
        font-size:.45rem;
    }
    a{
        color: #000;
    }
   .mint-indexlist-nav {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        background-color: red;
        border-left: 1px solid #ddd;
        text-align: center;
        -webkit-box-pack: center;
        -ms-flex-pack: center;
        justify-content: center;
    }
    .mint-cell{
        border-bottom: .01rem solid #f0f0f0!important; 
        font-size:.45rem;
    }
</style>
