# Vue在v-for中使用v-model绑定变量

## 界面展示部分

``` html

<div
  class="content-box-item"
  v-for="(item, index) in contentLists"
  :key="index"
>
  <div class="content-box-item-list">{{ item.title }}</div>
  <div class="content-box-item-list">
    <el-input
      :placeholder="item.placeholder"
      v-model="dataList[item.model]"
      :disabled="item.disable"
      clearable
    >
    </el-input>
  </div>
</div>

```

## data部分

``` javascript

//  数据部分
      dataList: {
        name: "MIX-iOS", //  产品名称
        version: "5037", //  版本号
        headMan: "李彩云", //  负责人
        storyCount: "30", //  故事点总数
        startTime: "2021-08-06", //  开始时间
        endTime: "2021-08-20", //  结束时间
        currentStatus: "1", //  当前情况 1 正常 2警告 3危险
        day: "2", // 剩余天数
        timelineList: [
          //  时间线
          {
            time: "2021-07-22",
            content: "需求评审",
          },
          {
            time: "2021-08-12",
            content: "版本提测",
          },
          {
            time: "2021-08-16",
            content: "版本提审",
          },
          {
            time: "2021-08-17",
            content: "提审通过",
          },
        ],
        //  功能点
        expoundList: [
          {
            content: "更新了XX功能",
          },
          {
            content: "更新了XX功能",
          },
          {
            content: "更新了XX功能",
          },
          {
            content: "更新了XX功能",
          },
        ],
      },
      //    输入框循环列表
      contentLists: [
        {
          title: "产品名称",
          placeholder: "请输入产品名称",
          model: "name",
          disable: true,
        },
        {
          title: "版本号",
          placeholder: "请输入版本号",
          model: "version",
          disable: false,
        },
        {
          title: "版本负责人",
          placeholder: "请输入版本负责人",
          model: "headMan",
          disable: false,
        },
        {
          title: "故事总点数",
          placeholder: "请输入故事总点数",
          model: "storyCount",
          disable: false,
        },
      ],
		}

```