<style>
  .avatar{
    width: 120px;
    height: 120px;
    border-radius: 50%;
  }
</style>
<template>
  <div class="app-container">
    <el-table v-loading="listLoading" :data="list" element-loading-text="Loading" border fit highlight-current-row>
      <el-table-column align="center" label="user_id" width="100">
        <template slot-scope="scope">
          {{ scope.row.user_id}}
        </template>
      </el-table-column>
      <el-table-column align="center" label="用户名" width="200">
        <template slot-scope="scope">
          {{ scope.row.nickName}}
        </template>
      </el-table-column>
      <el-table-column align="center" label="头像" width="200">
        <template slot-scope="scope">
          <img class="avatar" :src="scope.row.avatar" alt="">
        </template>
      </el-table-column>
      <el-table-column align="center" label="open_id" width="200">
        <template slot-scope="scope">
          {{ scope.row.open_id}}
        </template>
      </el-table-column>
      <el-table-column align="center" label="性别" width="200">
        <template slot-scope="scope">
          {{ scope.row.gender }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="创建时间">
        <template slot-scope="scope">
          {{ scope.row.creat_time }}
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
  import { getList } from '@/api/table'

  export default {
    filters: {
      statusFilter(status) {
        const statusMap = {
          published: 'success',
          draft: 'gray',
          deleted: 'danger'
        }
        return statusMap[status]
      }
    },
    data() {
      return {
        list: null,
        listLoading: true
      }
    },
    created() {
      this.fetchData()
    },
    methods: {
      fetchData() {
        var that=this
        this.listLoading = true
        setTimeout(() => {
          var arr = []
          for (var i = 0; i < 15; i++) {
            var obj = {
              user_id: i,
              avatar: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2088118308,646596224&fm=26&gp=0.jpg',
              nickName: '凉月' + (i + 1) + '号',
              open_id: 'qazzzz',
              creat_time: new Date().getTime(),
              gender: '男'
            }
            arr.push(obj)
          }
          that.list = arr
          console.log(arr)
          that.listLoading = false
        }, 1000);
      }
    }
  }
</script>