<style>
.richtext-box{
  border:none !important;
  overflow: hidden;
}
.richtext-body{
    padding:0 !important;
    margin: 0 !important;
    min-height: auto !important;
}
.richtext-body a[data-mention="true"] {
    cursor: text;
}
</style>

<template>
    <div class="simditor richtext-box">
        <div class="simditor-body richtext-body" v-html="value"></div>
        <span style="font-size:14px;color:#999" v-if="value==null||value==''">{{placeholder}}</span>
    </div>
</template>
<script>
export default {
    name:"RichtextLabel",
    props: ['value','placeholder'],
    data: function () {
        return {

        }
    },
    mounted:function(){
        this.addEvent();
    },
    methods:{
        addEvent(){
            var imgs = this.$el.getElementsByTagName("img");
            var imgSrcs=[];
            for(var i=0;i<imgs.length;i++){
                imgSrcs.push(imgs[i].src)
            }
            $(this.$el).on('click','img',function(e){
                var images =[];
                app.previewImages(e.currentTarget.src,imgSrcs)
            })
            $(this.$el).on('click','a',function(e){
                var url=$(this).attr('href');
                if(url.indexOf('http')!=-1){
                    window.open(url);
                }
                return false;
            })
        }
    }
}
</script>