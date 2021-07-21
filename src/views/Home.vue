<template>
  <div>
    <Cascader :list="list" :resultArr="resultArr"></Cascader>
  </div>
</template>

<script>
import Cascader from "@/views/Cascader.vue";
export default {
  name: "home",
  data() {
    return {
      list: [
        {
          id: 1,
          parentId: 0,
          value: 1,
          label: "卖家服务",
          lev: 1,
          children: [
            {
              id: 3,
              parentId: 1,
              value: 3,
              label: "中小学教辅",
              lev: 2,
              children: [
                {
                  id: 8,
                  parentId: 3,
                  value: 8,
                  label: "书法理论",
                  lev: 3,
                  children: [],
                },
                {
                  id: 9,
                  parentId: 3,
                  value: 9,
                  label: "书法赏析",
                  lev: 3,
                  children: [],
                },
                {
                  id: 10,
                  parentId: 3,
                  value: 10,
                  label: "字帖",
                  lev: 3,
                  children: [],
                },
                {
                  id: 11,
                  parentId: 3,
                  value: 11,
                  label: "技法/教程",
                  lev: 3,
                  children: [],
                },
                {
                  id: 12,
                  parentId: 3,
                  value: 12,
                  label: "硬笔书法",
                  lev: 3,
                  children: [
                    {
                      id: 13,
                      parentId: 4,
                      value: 13,
                      label: "4级菜单",
                      lev: 4,
                      children: [],
                    },
                  ],
                },
                {
                  id: 14,
                  parentId: 3,
                  value: 14,
                  label: "添加元素",
                  lev: 3,
                  children: [],
                },
                {
                  id: 15,
                  parentId: 3,
                  value: 15,
                  label: "添加元素",
                  lev: 3,
                  children: [],
                },
                {
                  id: 16,
                  parentId: 3,
                  value: 16,
                  label: "添加元素",
                  lev: 3,
                  children: [],
                },
              ],
            },
            {
              id: 4,
              parentId: 1,
              value: 4,
              label: "书法",
              lev: 2,
              children: [],
            },
            {
              id: 5,
              parentId: 1,
              value: 5,
              label: "传记",
              lev: 2,
              children: [],
            },
            {
              id: 6,
              parentId: 1,
              value: 6,
              label: "养生/保健",
              lev: 2,
              children: [],
            },
            {
              id: 7,
              parentId: 1,
              value: 7,
              label: "农业/林业",
              lev: 2,
              children: [],
            },
          ],
        },
        {
          id: 2,
          parentId: 0,
          value: 2,
          label: "图书",
          lev: 1,
          children: [],
        },
        {
          id: 17,
          parentId: 0,
          value: 17,
          label: "添加17",
          lev: 1,
          children: [],
        },
      ],
      resultArr: [],
    };
  },
  components: {
    Cascader,
  },
};
</script>