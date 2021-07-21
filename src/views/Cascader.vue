<template>
  <div id="cascader">
    <!-- 输入框 -->
    <input
      v-model="inputContent"
      @keyup.enter="search"
      placeholder="请输入搜索关键字"
    />
    <!-- 选择器 -->
    <div class="selectContent">
      <Select :list="list" :resultArr="resultArr"></Select>
    </div>
  </div>
</template>

<script>
import Select from "@/views/Select.vue";
export default {
  name: "cascader",
  components: {
    Select,
  },
  data() {
    return {
      inputContent: "",
      tempArr: [],
    };
  },
  created() {
    this.traverse(this.list);
  },
  props: ["list", "resultArr"],
  methods: {
    // 遍历 list 对象
    traverse(list) {
      for (let i = 0; i < list.length; i++) {
        this.tempArr.push(list[i]);
        if (list[i].children.length != 0) {
          this.traverse(list[i].children);
        }
      }
    },

    // 输入框的函数
    search() {
      for (let i = 0; i < this.tempArr.length; i++) {
        if (
          this.tempArr[i].label == this.inputContent &&
          this.judgment(this.inputContent)
        ) {
          this.tempArr[i].isShowChild = true;
          this.resultArr.push(this.tempArr[i]);
          console.log("已添加");
          console.log(this.resultArr);
        }
      }
    },

    // 检测当前查询的值是否已经添加过了
    judgment(content) {
      for (let i = 0; i < this.resultArr.length; i++) {
        if (this.resultArr[i].label === content) {
          return false;
        }
      }
      return true;
    },
  },
};
</script>

<style lang="less" scopd>
#cascader {
  margin-left: 50px;
  margin-top: 50px;
  input {
    width: 16rem;
    line-height: 1.8rem;
    border-radius: 0.2rem;
    border: 1px solid #dcdcdc;
    box-sizing: border-box;
    padding: 0 0 0 5px;
    margin-bottom: 5px;
    font-size: 15px;
  }
}
</style>