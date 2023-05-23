<template>
  <h1>关于我</h1>
  <p>hi, 我是yukangyang，一名前端开发。</p>
  <p>
    两年前端开发经验
  </p>
  <p>
    你可以在这里找到我：
    <a v-for="(link, index) of links" :key="link.text" :href="link.href">
      {{ `${link.text} ${index + 1 < links.length ? "、" : ""}` }}
    </a>
  </p>

  <p>邮箱：3360947218@qq.com</p>
  <p>微信：s1872156</p>
</template>

<script lang="ts" setup>
const links = [
  {
    text: "github",
    href: "https://github.com/yukangyang",
  },
  {
    text: "哔哩哔哩",
    href: "https://space.bilibili.com/388476777",
  },
];
</script>

<style></style>
