<template>
  <div>
    <h3>
      重写Example02组件，视图不变，从setup()函数中分离出独立的逻辑函数执行
    </h3>
    <!-- 将user对象的属性绑定到视图 -->
    <p>显示中文：{{ sentenceRef?.chinese }}</p>
    <p>显示英文：{{ sentenceRef?.english }}</p>
    <p>
      ↓↓↓computed()函数，当user对象改变时，重新计算user对象中的english属性↓↓↓
    </p>
    <!-- 将计算属性绑定到视图 -->
    <p>英文大写：{{ upperSentence }}</p>
    <!-- 将change函数绑定到按钮 -->
    <button type="button" @click="change">点击回答</button>
    <p>（点击按钮即可改变user对象）</p>
  </div>
</template>
<script lang="ts">
import { computed, defineComponent, Ref, ref } from "vue";

// 声明约束接口
interface Sentence {
  chinese?: string;
  english?: string;
}

// 独立的与user相关的业务逻辑
function useSentence(stc: Ref<Sentence>) {
  // 创建计算属性，当响应式数据改变时自动改变
  const upperSentence = computed(() => stc.value.english?.toUpperCase());
  // 创建change函数，改变响应式属性的值
  const change = () => {
    stc.value.chinese = "我很好，谢谢！";
    stc.value.english = "I'm fine, thank you!";
  };
  // 将此逻辑实现的1个计算属性，1个执行函数封装在对象中返回，无需声明use函数返回类型
  return {
    upperSentence,
    change
  };
}

export default defineComponent({
  setup() {
    // 创建接口类型对象
    const sentence: Sentence = {
      chinese: "你好吗？",
      english: "How are you?"
    };
    // 创建响应式对象
    const sentenceRef = ref(sentence);
    // 调用独立逻辑函数
    const { upperSentence, change } = useSentence(sentenceRef);
    // 返给视图
    return {
      sentence,
      sentenceRef,
      upperSentence,
      change
    };
  }
});
</script>
