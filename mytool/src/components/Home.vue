<template>
  <div>
    <el-container>
      <el-header style=" height: 60px">
        <el-dropdown placement="top">
          <span class="el-dropdown-link">
            CosPlay<i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">真人Play</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-header>

      <el-container>
        <el-main>
          <el-row :gutter="20">
            <el-col :span="8"><div class="grid-content bg-purple-dark imageContent1">
              <el-row :gutter="20">
                <el-col :span="12"><div class="grid-content bg-purple">
                  <el-image :src="src"></el-image>
                </div></el-col>
                <el-col :span="12"><div class="grid-content bg-purple">
                  <el-image :src="src"></el-image>
                </div></el-col>
              </el-row>
            </div></el-col>
            <el-col :span="16"><div class="grid-content bg-purple-dark">
              <span class="demonstration">默认 Hover 指示器触发</span>
              <el-carousel height="150px">
                <el-carousel-item v-for="item in 4" :key="item">
                  <h3 class="small">{{ item }}</h3>
                </el-carousel-item>
              </el-carousel>
            </div></el-col>
          </el-row>

        </el-main>
        <el-aside>Aside</el-aside>
      </el-container>
      <el-footer>Footer</el-footer>
    </el-container>
  </div>
</template>

<script>
    export default {
      data() {
        return {
          src: 'https://cube.elemecdn.com/6/94/4d3ea53c084bad6931a56d5158a48jpeg.jpeg'
        }
      },
        name: "Home"
    }
</script>

<style scoped>
  .el-header{
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  .el-footer {
    background-color: #B3C0D1;
    color: #333;
    /*text-align: center;*/
    line-height: 60px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    height: 1500px;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    height: 1500px;
  }

  .el-image{
    height: 170px;
    /*vertical-align:middle;*/
  }

  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>
