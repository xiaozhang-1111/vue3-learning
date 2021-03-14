<template>
  <div>
    <h1>data()</h1>
    <!-- 视图绑定 -->
    <p>
      {{ message }}
    </p>
    <hr />
    <h1>methods</h1>
    <!-- 声明绑定视图按钮 -->
    <button type="button" @click="change">点击显示中文</button>
    <hr />
    <h1>computed</h1>
    <!-- 计算属性绑定视图 -->
    <p>数据长度：{{ length }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  // 声明响应式属性
  data: () => ({
    message: "Hello, world!"
  }),
  // 声明修改响应式属性数据方法
  methods: {
    change() {
      this.message = "你好，世界！";
    }
  },
  // 声明计算属性，计算响应式属性数据的长度
  computed: {
    length(): number {
      return this.message.length;
    }
  }
});
</script>
