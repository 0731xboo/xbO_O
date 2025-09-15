<!-- ---

title: vitepress vue
descrtiption: vitepress在md文档中使用vue语法demo
sticky: 3
top: 3

--- -->


<!-- # vue -->

<script setup>
import {useData} from 'vitepress';


const page = useData()

</script>

## Markdown Content

<pre>{{page}}</pre>
