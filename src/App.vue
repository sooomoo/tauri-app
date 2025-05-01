<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
  greetMsg.value = await invoke("greet", { name: name.value });
}
</script>

<template>
  <header data-tauri-drag-region class="header">
    <span>实时聊天是通过WebSocket来实现</span>
  </header>
  <main class="main">
    Welcome to Tauri + Vue

    <form class="row" @submit.prevent="greet">
      <input id="greet-input" v-model="name" placeholder="Enter a name..." />
      <button type="submit">Greet</button>
    </form>
    <p>{{ greetMsg }}</p>
    <p>
      刚接到的一个售前在线咨询的需求，实时聊天是通过WebSocket来实现。但是用户打开多个页面同时又在其他标签页打开咨询窗口的时候ws也会多开一个，就导致几个tab页互相抢ws连接。我就想能不能将一个页面的ws消息共享给其他页面，于是就想到了SharedWorker，并且兼容性不错（IE已死，不用怕）。
    </p>
  </main>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 36px; 
  user-select: none;
  z-index: 2;
  display: flex;
  align-items: center;
  padding: 0 16px;
  font-weight: bold;
}
.main {
  position: fixed;
  top: 36px;
  left: 0;
  right: 0;
  bottom: 0;
  padding: 16px;
  z-index: 0;
}


</style>
<style>

html,body {
  margin: 0;
  padding: 0; 
  background: transparent; 
}

body {
  font-family: 'AlibabaPuHuiTi';
  color: #333;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;
  font-size: 14px;
}

.row {
  display: flex;
  justify-content: center;
}


</style>