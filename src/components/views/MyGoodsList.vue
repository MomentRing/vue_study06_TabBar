<template>
  <div>
    <MyTable :arr="list">
      <template #header>
        <th>#</th>
        <th>商品名称</th>
        <th>价格</th>
        <th>标签</th>
        <th>操作</th>
      </template>

      <template #body="scope">
        <td>{{ scope.row.id }}</td>
        <td>{{ scope.row.goods_name }}</td>
        <td>{{ scope.row.goods_price }}</td>
        <td>
          <input
            class="tag-input form-control"
            style="width: 100px"
            type="text"
            v-if="scope.row.inputVisible"
            v-focus
            @blur="scope.row.inputVisible = false"
            @keyup.enter="enterFn(scope.row)"
            @keyup.esc="scope.row.inputValue = ''"
            v-model="scope.row.inputValue"
          />
          <button
            v-else
            style="display: block"
            class="btn btn-primary btn-sm add-tag"
            @click="scope.row.inputVisible = true"
          >
            +Tag
          </button>
          <span v-for="(str, ind) in scope.row.tags" :key="ind">
            {{ str }}
          </span>
        </td>
        <td>
          <button
            class="btn btn-danger btn-sm"
            @click="removeBtn(scope.row.id)"
          >
            删除
          </button>
        </td>
      </template>
    </MyTable>
  </div>
</template>

<script>
import MyTable from '../MyTable.vue'
import axios from 'axios'
axios.defaults.baseURL = 'https://applet-base-api-t.itheima.net'
export default {
  created() {
    axios({
      url: '/api/goods',
    }).then((res) => {
      console.log(res.data.data)
      this.list = res.data.data
    })
  },
  data() {
    return {
      list: [],
    }
  },
  methods: {
    removeBtn(id) {
      let index = this.list.findIndex((obj) => obj.id === id)
      this.list.splice(index, 1)
    },
    enterFn(obj) {
      if (obj.inputValue.trim().length === 0) {
        return alert('请输入数据')
      }
      obj.tags.push(obj.inputValue)
      obj.inputValue = ''
    },
  },
  computed: {},
  watch: {},
  filters: {},
  components: {
    MyTable,
  },
}
</script>

<style lang="less" scoped>
.my-goods-list {
  .badge {
    margin-right: 5px;
  }
}
</style>
