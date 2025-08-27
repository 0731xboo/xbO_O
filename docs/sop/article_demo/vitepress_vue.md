---
title: vitepress vue
description: vitepress 文章中使用vue语法示例
tag: demo
top: 2
---

# vitepress md文件中使用vue

<script setup>
 import {useData} from 'vitepress';
 import {ref} from 'vue';

 const {page}  = useData();
 const count = ref(1);
</script>


## markdown 内容
 计数器:{{count}}
<pre>{{page}}</pre>

<button :class="$style.button" @click="count++">Increment</button>

<!--  如果需要使用css 预处理器,需要先安装相应的预处理器,如sass -->
<style>
    .button{
     color:blue;
    }
</style>



