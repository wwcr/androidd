<template>
  <div style="padding-top:1.25rem;">
    <uploader
      url="http://h5.wwcrpt.com/index.php/index/api/content_up"
    ></uploader>
    
    <div class="btn" @click="upload">提交</div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import units from '../tools/units'
export default {
  data () {
    return {
      imgs: [],
    }
  },
  computed: {
    ...mapState({
      imgStatus: state => state.imgstore.img_status,
      imgPaths: state => state.imgstore.img_paths
    })
  },
  methods: {
    upload () {
      this.$store.commit('set_img_status', 'uploading')
    },
    submit () {
      let values = []
      for (let key of this.imgPaths) {
        values.push(key)
      }
      this.imgs = values
    }
  },
  watch: {
    imgStatus () {
      if (this.imgStatus === 'finished') {
        this.submit()
      }
    }
  },
  destoryed () {
    this.imgs = []
  },
  created () {
    units.title.set('发表内容');
    
  } 
}
</script>

<style scoped lang="less">
.btn {
  width:80%;
  height: 3em;
  margin-left:10%; 
  font-size: .3rem;
  background-color: green;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>