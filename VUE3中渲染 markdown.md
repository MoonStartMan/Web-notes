# VUE3中渲染 markdown

## 安装相关插件

``` shell
pnpm add v-md-editor
```

## 创建 MarkDown.vue 组件

### template中

``` vue
<template>
    <span v-html="markdownDom"></span>
</template>
```

### script中

``` vue
<script setup>
import { watchEffect, ref } from 'vue'
import MarkdownIt from 'markdown-it'
import markdownItHighlightjs from 'markdown-it-highlightjs'
import markdownItCodeCopy from 'markdown-it-code-copy'

const props = defineProps({
    markdownText: {
        type: String,
        required: true,
    }
})

// 用于存放最终解析出来的dom
const markdownDom = ref('')
// 初始化 markdown-it 实例
const md = new MarkdownIt()
// 配置代码高亮插件
md.use(markdownItHighlightjs)
// 配置代码块复制插件
md.use(markdownItCodeCopy)
// 解析markdown
const handleMarkdown = () => {
    // 判断markdown为空不解析
    if (!props.markdownText) {
        return
    }
    // 解析markdown获取HTML
    const html = md.render(props.markdownText)
    markdownDom.value = html
}

watchEffect(() => {
    handleMarkdown()
})
</script>

```

## 外部使用

``` vue

import MarkDown from '../compoents/MarkDown.vue'

<MarkDown :markdownText="content">

```

