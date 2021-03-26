<template>
  <div>
    <!-- 将user对象的属性绑定到视图 -->
    <p>显示中文：{{ sentenceRef?.chinese }}</p>
    <p>显示英文：{{ sentenceRef?.english }}</p>
    <p>
      ↓↓↓computed()函数，当user对象改变时，重新计算user对象中的english属性↓↓↓
    </p>
    <!-- 将计算属性绑定到视图 -->
    <p>英文大写：{{ sentenceComputed }}</p>
    <!-- 将change函数绑定到按钮 -->
    <button type="button" @click="change">点击回答</button>
    <p>（点击按钮即可改变user对象）</p>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";

// 声明约束接口
interface Sentence {
  chinese?: string;
  english?: string;
}

export default defineComponent({
  setup() {
    // 创建接口类型对象
    const sentence: Sentence = {
      chinese: "你好吗？",
      english: "How are you?"
    };
    const sentenceAsync: Sentence = {
      chinese: "我很好，谢谢你！",
      english: "I'm fine, thank you!"
    };
    // 创建响应式对象
    const sentenceRef = ref(sentence);
    // 创建computed()函数，绑定对象中的指定属性
    const sentenceComputed = computed(() =>
      sentenceRef.value.english?.toUpperCase()
    );
    // 创建函数change，修改对象中的属性，从而可测试计算属性效果
    const change = () => {
      sentenceRef.value = sentenceAsync;
    };

    return {
      sentence,
      sentenceAsync,
      sentenceRef,
      sentenceComputed,
      change
    };
  }
});
</script>
