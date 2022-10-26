<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import liff from '@line/liff';
import axios from 'axios'
import { ref } from '@vue/reactivity';
console.log(import.meta.env.VITE_liffid)
liff.init({ liffId: import.meta.env.VITE_liffid }).then(async() => {
　console.log('初始化成功');
  console.log(liff.getOS())
  if (!liff.isLoggedIn()) {
   alert("用戶未登入");
   liff.login();

  } else{
    let userID = await liff.getProfile()
      let url = (await runCode()).value
      if(!url){
        window.close();
        return;
      }
      await axios.post(import.meta.env.VITE_host,{url,line:userID})
      liff.openWindow({
        url,
        external:true
      })
  }

}).catch((err) => {
  alert("Line登入元件初始化失敗");
  window.close();
});;

async function runCode(){
    return liff.scanCodeV2()

}
const msg = ref("");
</script>

<template>
  <p>編譯器說這裡沒東西他會不開心會error，所以我只好加了。<br/>看到這訊息代表請關閉此頁面，你可能bug了或執行完畢了。</p>
  <!-- <button @click="runCode">執行相機</button> -->

  <!-- {{msg}} -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
