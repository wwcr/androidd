<!--页面css样式-->
<style scoped lang='scss'>
    .findcar {
        padding: 0.4rem;
      background: #fff;
    }

    .findcar h3 {
        color: #1e1e1e;
        font-size: 0.7rem;
        font-weight: normal;
        font-weight: 700;
        padding-top:$top; 
    }

    .new {
        margin-top: 0.3rem;
        display: flex;
    }

    .new .p1 {
        color: #ccc;
        font-size: 0.3rem;
        display: block;
        flex: 1;
    }

    .new .p2 {
        display: block;
        font-size: 0.2rem;
        color: #999;
        flex: 1;
        text-align: right;
    }

    .new .p2 span {
        color: #999;
        border: 1px solid #999;
        font-size: 0.28rem;
        border-radius: 3px;
        padding: 0.05rem 0.1rem;
    }

    .article {
        font-size: 0.4rem;
        color: #1e1e1e;
        line-height: 0.7rem;
        margin-top: 0.4rem;
        letter-spacing: 0.01rem;
        font-weight: 300;
    }

    .cont_div img {
        width: 100%;
        margin: 0.3rem 0;
    }
    .commit img{
        width: 100%;
    }
</style>
<template>
    <!--行业新闻  -->
    <div>
        <div id="Findcar" class="findcar" v-if='article.art_content'>
            <h3 v-if='article.art_title'>{{article.art_title}}</h3>
            <div class="new">
                <p class="p1"><span v-if='article.art_time'>{{article.art_time}}</span><span v-if='article.cate_name'>&nbsp;{{article.cate_name}}</span></p>
                <p class="p2" v-if='article.art_title'>阅读&nbsp;{{Math.ceil(Math.random()*1000)}}</p>
            </div>
            <div class="cont_div" @click='openImageProxy($event)'>
                <p v-if='article.art_desc' class="article" v-html="article.art_desc"></p>
                <img v-if='article.art_thumb' :src="host+article.art_thumb">
                <p v-if='article.art_content' class="article" v-html="article.art_content"></p>
            </div>
        </div>
        <div class="commit" @click="commit" v-if="false">
            <img src="../../assets/img/commit.jpg">
        </div>
    </div>
</template>
<script>
    
    import units from '../../tools/units'
    export default {
        data () {
            return {
                article: [],
                aid: '',
                host:units.getHost()
            }
        },
        methods: {
            openImageProxy(e) {
                if(e.target.nodeName === 'IMG') {
                   layer.open({
  type: 1,
  skin: 'layui-layer-rim', //加上边框
  area: ['420px', '240px'], //宽高
  content: 'html内容'
});
                }
            },
            timeer: function (time) {
                return units.timemake(time)
            },
            more(){
                this.getArticle();
            },
            commit:function () {
                layer.msg('近期开放')
            },
            moreThatText: function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            getArticle(){
                let that = this;
                this.$http.post(units.host('article'), units.paramsno({
                    swt: 'content',
                    id: this.aid
                })).then(function (res) {
                    if(!res.data.warning) {
                        this.article = res.data.info;
                    }else { 
                        layer.msg(res.data.warning);
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
                });
            }
        },
        created: function () {
            this.aid = this.$route.query.id;
            this.getArticle();
            units.title.set('无维易寻');
        }
    }
</script>
