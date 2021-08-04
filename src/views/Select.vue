<template>
  <ul class="select">
    <li class="special"><input type="checkbox" @click="check($event,list)" /></li>
    <!-- 每一个小的项 -->
    <li v-for="(item, index) in list" :key="index">
      <!-- 点击每一项之后执行函数 -->
      <div class="listName" @click="changeList(item, index)">
        <!-- 每一项的名字 点击之后变色 -->
        <span
          :class="{ clicked: item.isShowChild && item.children.length === 0 }"
        >
          {{ item.label }}
        </span>
        <div
          v-show="item.children && item.children.length > 0"
          style="position: absolute; right: 1rem; height: 100%"
        >
          <span v-show="!item.isShowChild">&#62;</span>
          <span
            v-show="item.isShowChild"
            :class="{ clicked: item.isShowChild && item.children.length === 0 }"
            >&#62;</span
          >
        </div>
      </div>
      <!-- 子列表ul -->
      <div
        class="children"
        v-show="item.isShowChild && item.children && item.children.length > 0"
      >
        <Select :list="item.children" :resultArr="resultArr" :isSelect="isSelect"></Select>
      </div>
    </li>
  </ul>
</template>

<script>
import Select from "@/views/Select";

export default {
  name: "Select",

  data() {
    return {
      isShowList: false,
      arr:[],
    };
  },

  components: {
    Select,
  },

  props: ["list", "resultArr","isSelect"],

  methods: {
    changeList(item) {
      // 点击每一个项
      if (item.children.length == 0 && !item.isShowChild) {
        this.resultArr.push(item);
        console.log(this.resultArr);
      }

      // 如果没有就设置为 true 如果有了就设置为相反的
      if (item.hasOwnProperty("isShowChild")) {
        item.isShowChild = !item.isShowChild;
      } else {
        this.$set(item, "isShowChild", true);
      }

      // 点击完之后，如果 这一项变暗
      if (!item.isShowChild) {
        // 关闭当前项，不展示子项，执行 childStatus 函数
        this.childStatus(item);
        // 在数组中删除此项  判断该项为末项
        if (item.children.length == 0) {
          this.delete(item.id);
        }
      }
    },

    //如果子列表的子列表被展开，点击父列表关闭时，子列表的子列表也应该被关闭
    childStatus(item) {
      // 没有子元素的化
      if (!item.children || item.children.length < 1) {
        return;
      }
      // 还有子元素
      for (let i = 0; i < item.children.length; i++) {
        // 因为每一级列表只会有一个展开项，因此只需要找到展开项 递归执行关闭功能
        if (item.children[i].isShowChild) {
          if (!item.children[i].isShowChild) {
            item.children[i].isShowChild = false;
          }
          this.childStatus(item.children[i]);
          break;
        }
      }
    },

    // 删除数组中的一项
    delete(id) {
      for (let i = 0; i < this.resultArr.length; i++) {
        if (this.resultArr[i].id === id) {
          this.resultArr.splice(i, 1);
          console.log(this.resultArr);
        }
      }
    },

    // 多选框被选中
    check(e,list) {
      if(e.target.checked){
        console.log(e.target.checked)
        list.forEach((item) => {
          if(item.children.length === 0 && this.judge(item)){
            this.resultArr.push(item)
          }else{
            this.check(e,item.children)
          }
        })
        console.log(this.resultArr)
      }else{
        console.log(e.target.checked)
        for(let i = 0;i < this.resultArr.length;i++){
          for(let j = 0;j < list.length;j++){
            if(this.resultArr[i].id === list[j].id){
              this.resultArr.splice(i,1)
            }
          }
        }
        console.log("删除数组中的元素")
        console.log(this.resultArr)
      } 
    },

    // 判断当前的数组中有没有这个元素
    judge(element){
      for(let i = 0;i < this.resultArr.length;i++){
         if(element.id === this.resultArr[i].id){
          return false
        }
      }
      return true
    }

  },
};
</script>

<style lang="less" scoped>
.select {
  height: 187px;
  margin: 0;
  padding: 0;
  position: fixed;
  top: 90px;
  border: 1px solid #e4e7ed;
  border-radius: 0.2rem;
  overflow-y: auto;
}

.select li {
  position: relative;
  width: 10rem;
  list-style: none;
  text-align: center;
  line-height: 2rem;
  margin: 0;
  box-sizing: border-box;
  padding: 0 0 0 2rem;
  display: flex;
  flex-direction: row;
  //禁止元素的文字被选中
  -moz-user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}
ul li:hover {
  background: #dcdcdc;
}
.clicked {
  color: #1e90ff;
}
.listName {
  display: flex;
  width: 100%;
  cursor: pointer;
}
.children {
  position: absolute;
  right: 0px;
  height: 0px;
  padding: 0px;
}
// 设置比较细的滚动条
::-webkit-scrollbar {
  width: 3px;
}
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}
::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.15);
}
// 多选框
input {
  height: 16px;
  padding-top: 8px;
  display: inline-block;
}
.special {
  line-height: 32px;
  height: 32px;
  position:fixed;
}
.special:hover {
  background-color: #fff;
}
</style>