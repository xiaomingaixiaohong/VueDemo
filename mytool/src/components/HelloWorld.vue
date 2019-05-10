<template>
  <div class="hello">
    <el-upload
      class="upload-demo"
      :action="upload()"
      :on-preview="handlePreview"
      :on-remove="handleRemove"
      :on-success="success"
      :before-remove="beforeRemove"
      multiple
      :limit="3"
      :on-exceed="handleExceed"
      :file-list="fileList">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>

    <el-button @click="resolveProblem" type="primary">开始解析</el-button>
    <!--<h1>{{ msg }}</h1>-->
    <!--<h2>Essential Links</h2>-->
    <!--<ul>-->
      <!--<li>-->
        <!--<a-->
          <!--href="https://vuejs.org"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--Core Docs-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="https://forum.vuejs.org"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--Forum-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="https://chat.vuejs.org"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--Community Chat-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="https://twitter.com/vuejs"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--Twitter-->
        <!--</a>-->
      <!--</li>-->
      <!--<br>-->
      <!--<li>-->
        <!--<a-->
          <!--href="http://vuejs-templates.github.io/webpack/"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--Docs for This Template-->
        <!--</a>-->
      <!--</li>-->
    <!--</ul>-->
    <!--<h2>Ecosystem</h2>-->
    <!--<ul>-->
      <!--<li>-->
        <!--<a-->
          <!--href="http://router.vuejs.org/"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--vue-router-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="http://vuex.vuejs.org/"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--vuex-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="http://vue-loader.vuejs.org/"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--vue-loader-->
        <!--</a>-->
      <!--</li>-->
      <!--<li>-->
        <!--<a-->
          <!--href="https://github.com/vuejs/awesome-vue"-->
          <!--target="_blank"-->
        <!--&gt;-->
          <!--awesome-vue-->
        <!--</a>-->
      <!--</li>-->
    <!--</ul>-->

    <!--<el-container>-->
      <!--<el-main style=" line-height: 150px;background-color: darkgreen">-->
        <!--<div class="block">-->
          <!--<span class="demonstration">默认 Hover 指示器触发</span>-->
          <!--<el-carousel height="150px">-->
            <!--<el-carousel-item v-for="item in 4" :key="item">-->
              <!--<h3 class="small">{{ item }}</h3>-->
            <!--</el-carousel-item>-->
          <!--</el-carousel>-->
        <!--</div>-->
      <!--</el-main>-->

      <!--<el-aside style=" width:40%;line-height: 150px;background-color:cornflowerblue">-->
        <!--<div class="block">-->
          <!--<span class="demonstration">默认 Hover 指示器触发</span>-->
          <!--<el-carousel height="150px">-->
            <!--<el-carousel-item v-for="item in 4" :key="item">-->
              <!--<h3 class="small">{{ item }}</h3>-->
            <!--</el-carousel-item>-->
          <!--</el-carousel>-->
        <!--</div>-->
      <!--</el-aside>-->
    <!--</el-container>-->



  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      fileList: [],
      nameList:[]
    };
  },
  methods: {
    handleRemove(file, fileList) {
      //console.log(file, fileList);
      var names =this.nameList;
      for ( var i = 0; i <names.length; i++){
        if(file.name ==names[i].upName){
          this.nameList.splice(i,1);
          return;
        }
      }
      // console.log(this.nameList);
    },
    handlePreview(file) {
      console.log(file);
    },
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    beforeRemove(file, fileList) {
      return this.$confirm(`确定移除 ${ file.name }？`);
    },
    upload(){
     return this.$http.defaults.baseURL + "/upload"
    },
    success(response, file, fileList){
      //8/alert(response);
      var name ={upName:response.upName,localName:response.localName};
      this.nameList.push(name);
      console.log( this.nameList);

    },
    resolveProblem(){
      alert(111);
      this.$http.post('resolveProblem', {nameList:this.nameList})
        .then((res) => {
          console.log("查询button的数据end...")
          console.log(res)
          $self.buttons =res.data.buttons;
        })
        .catch((err) => {
          console.log(err)
          console.log('提交失败！')
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
