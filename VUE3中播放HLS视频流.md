# VUE3中播放HLS视频流

## 安装vue3-video-play

``` shell
pnpm add vue3-video-play
```

## 局部使用

``` javascript
import { videoPlay } from 'vue3-video-play';
```

**如果找不到vue3-video-play的处理方法**

``` txt
1. 在node_modules 里面找到 vue3-video-play
2. 修改 package.json 文件
3. 找到 moudle 一栏 -> 修改为 "./dist/index.mjs"

```

## 创建 videoPlay

``` vue
<videoPlay
  ref="videoElement"
  width="600px"
  :src="options.src"
  :type="options.type"
  :autoPlay="true"
  :muted="true"
  :control="false"
  @error="handleError"
  @loadedmetadata="handleLoadedMetadata"
  @canplay="handleCanPlay"
  @play="handlePlay"
  @pause="handlePause"
/>

```

## 在 script 中添加相应的方法

``` vue

<script setup>
import { onMounted, ref, reactive, nextTick } from "vue";
import { videoPlay } from 'vue3-video-play';

const props = defineProps({
  src: {
    type: String,
    required: true,
  },
});

const options = reactive({
  src: props.src,
  type: "m3u8",
});

const videoElement = ref(null);

const handleError = (event) => {
  console.error("Error event:", event);
};

const handleLoadedMetadata = (event) => {
  console.log("Loaded metadata:", event);
};

const handleCanPlay = (event) => {
  console.log("Can play event:", event);
  videoElement.value.play().catch((error) => {
    console.error("Error playing video:", error);
  });
};

const handlePlay = (event) => {
  console.log("Play event:", event);
};

const handlePause = (event) => {
  console.log("Pause event:", event);
};

onMounted(() => {
  nextTick(() => {
    if (videoElement.value) {
      videoElement.value.play().catch((error) => {
        console.error("Error playing video on mounted:", error);
      });
    }
  });
});
</script>

```