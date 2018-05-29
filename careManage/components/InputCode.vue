<template>
<!-- 交接中输入验证码 -->
    <div class="input-code-mark">
        <div class="input-code-box">
            <div class="input-code">
                <h5>请输入交车验证码</h5>
                <!-- <div class="box">
                    <div class="pawDiv"><input type="number" class="paw" maxlength="1"></div>
                    <div class="pawDiv"><input type="number" class="paw" maxlength="1"></div>
                    <div class="pawDiv"><input type="number" class="paw" maxlength="1"></div>
                    <div class="pawDiv"><input type="number" class="paw" maxlength="1"></div>
                    <div class="pawDiv"><input type="number" class="paw" maxlength="1"></div>
                    <div class="pawDiv"><input type="number" class="paw bRight" maxlength="1"></div>
                </div> -->
                <vue-input-code span-size="20px" :upper-case="true" type="number" :number="6" height="40px" span-color="#f35252" input-color="#f35252" input-size="20px" :error="error" :code="code4" :get-input="getInput" :success="success"></vue-input-code>

                <div class="errorWarn"><slot></slot></div>
                <div class='btn' @click.stop="sureCode(1)"><button></button></div>
            </div>
            <div class="close-x" @click="sureCode(0)">
                <img src="../../../assets/img/xxxx.png" alt="">
            </div>
        </div>
    </div>
</template>

<script>
// import VueInputCode from 'vue-input-code'
export default {
    data () {
        return {
            info: '123456', //验证码
            code4: [],
        }
    },
    methods: {
        success(code){
          this.info = code;
          console.log('success',code, this.info);
        },
        getInput(code){
          this.input = code;
        },
        error(code){
          console.log("错误输入:",code);
          return true;
        },
        
        sureCode (val) {
            // this.getPassword();
            this.$emit('sureCode', {val:val, info: this.info})
        },
        // getPassword (){
        //     var n="";
        //     var pawDiv=document.getElementsByClassName("pawDiv");
        //     var paw=document.getElementsByClassName("paw");
        //     var pawDivCount=pawDiv.length;
        //     for(var i=0;i<pawDivCount;i++){
        //         n+=paw[i].value;
        //     }
        //     this.info = n;
        //     // console.log(that.info)
        //     // layer.msg(n);
        // }
    },
    components: {
        // VueInputCode
    },
    
    // mounted () {

    //     let that = this;
    //     var pawDiv=document.getElementsByClassName("pawDiv");
    //     var paw=document.getElementsByClassName("paw");
    //     var pawDivCount=pawDiv.length;
    //     /*设置第一个输入框默认选中*/
    //     // pawDiv[0].setAttribute("style","border: .02rem solid deepskyblue;");
    //     paw[0].readOnly=false;
    //     paw[0].focus();
        
    //     // // var errorPoint=document.getElementsByClassName("errorPoint")[0];
    //     /*绑定pawDiv点击事件*/
 
    //     function func(){
    //         for(var i=0;i<pawDivCount;i++){
    //             // console.log(pawDiv[i])
    //             // pawDiv[i].addEventListener("click",function(){
    //             //     pawDivClick(this);
    //             // });
    //         paw[i].onkeyup=function(event){
    //         if(event.keyCode>=48&&event.keyCode<=57){
    //             /*输入0-9*/
    //             changeDiv();
    //             // errorPoint.style.display="none";
            
    //         }else if(event.keyCode=="8") {
    //             /*退格回删事件*/
    //             firstDiv();
            
    //         }else if(event.keyCode=="13"){
    //             /*回车事件*/
    //             getPassword();
            
    //         }else{
    //             /*输入非0-9*/
    //             // errorPoint.style.display="block";
    //             this.value="";
    //         }
            
    //         };
    //         }
            
    //         }
    //         func();
    
    
    //         /*定义pawDiv点击事件*/
    //         // var pawDivClick=function(e){
    //         // for(var i=0;i<pawDivCount;i++){
    //         // pawDiv[i].setAttribute("style","border:none");
    //         // }
    //         // e.setAttribute("style","border: .02.02rem solid deepskyblue;");
    //         // };
            
            
    //         /*定义自动选中下一个输入框事件*/
    //         var changeDiv=function(){
    //         for(var i=0;i<pawDivCount;i++){
    //             if(paw[i].value.length=="1"){
    //                 /*处理当前输入框*/
    //                 paw[i].blur();
                    
    //                 /*处理上一个输入框*/
    //                 paw[i+1].focus();
    //                 paw[i+1].readOnly=false;
    //                 // pawDivClick(pawDiv[i+1]);
    //             }
    //         }
    //         };
            
    //         /*回删时选中上一个输入框事件*/
    //         var firstDiv=function(){
    //         for(var i=0;i<pawDivCount;i++){
    //             console.log(i);
    //             if(paw[i].value.length=="0"){
    //                 /*处理当前输入框*/
    //                 console.log(i);
    //                 paw[i].blur();
                    
    //                 /*处理上一个输入框*/
    //                 paw[i-1].focus();
    //                 paw[i-1].readOnly=false;
    //                 paw[i-1].value="";
    //                 // pawDivClick(pawDiv[i-1]);
    //                 break;
    //                 }
    //             }
    //         };
    
    //         /*获取输入密码*/
    //         // var getPassword=function(){
    //         //     var n="";
    //         //     for(var i=0;i<pawDivCount;i++){
    //         //         n+=paw[i].value;
    //         //     }
    //         //     that.info = n;
    //         //     // console.log(that.info)
    //         //     layer.msg(n);
    //         // };
    //         // var getPasswordBtn=document.getElementsByClassName("getPasswordBtn")[0];
            
    //         // getPasswordBtn.addEventListener("click",getPassword);
            
    //         /*键盘事件*/
    //         document.onkeyup=function(event){
    //             if(event.keyCode=="13") {
    //                 /*回车事件*/
    //                 getPassword();
    //             }
    //         };
    // }
}
</script>

<style lang='scss' scoped>
.bRight{
    border-right: 0px dashed #ccc!important;
}
.box{
    margin: 0 auto;
    width: 6.06rem;
    height: 1rem;
    border:1px solid #ccc;
    line-height: 1rem;
    display: flex;
    margin-bottom:.8rem; 
}
.box input.paw{
 width: 1rem;
 height: .35rem;
 padding: .4rem 0;
 margin-left: -9px;
 border:none;
 border-right: 1px dashed #ccc;
 text-align: center;
}
.box input.paw:nth-child(1){
 margin-left: 0;
}
.content .box input.paw:focus{outline:0;}
.content .box .pawDiv{
    display: inline-block;
    line-height: 1rem;
    width: 1rem;
    height: 1.2rem;
    flex:1;
}


.input-code-mark{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .5);
    z-index: 999; 
    .input-code-box{
        width: 8rem;
        position: absolute;
        top: 25%;
        background: #fff;
        margin-left: 50%;
        transform: translateX(-50%);
        border-radius: .08rem;
        padding-bottom:.6rem; 
        .close-x{
            position: absolute;
            bottom:-1.8rem;
            margin-left: 50%;
            transform: translateX(-50%);
        }
        .input-code{
            padding: 0 .45rem;
            text-align: center;
            h5{
                padding-top: .2rem;
                line-height: 1.8rem;
            }
            .errorWarn{
                color: #ff8d55;
                font-size: .35rem;
                margin-top:.4rem; 
            }
            .btn{
                margin-top : .45rem;
                width: 100%;
                height: 1.4rem;
                border-radius: .08rem;
                button{
                    width: 100%;
                    height: 100%;
                    outline: none;
                    border-radius: .08rem;
                    border: 0;
                    background: url('../../../assets/img/btn-sure.png') center no-repeat;
                    background-size: 100%;
                }
            }
        }
    }
}

</style>
