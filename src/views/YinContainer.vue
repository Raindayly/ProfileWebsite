<template>
  <home></home>
</template>

<script lang="ts">
import {defineComponent,getCurrentInstance, onBeforeMount, onMounted } from "vue";

import Home from "@/views/Home.vue";
export default{
  components: { Home },
  setup(){
    const { proxy } = getCurrentInstance();

    if (sessionStorage.getItem("dataStore")) {
      proxy.$store.replaceState(Object.assign({}, proxy.$store.state, JSON.parse(sessionStorage.getItem("dataStore"))));
    }

    window.addEventListener("beforeunload", () => {
      sessionStorage.setItem("dataStore", JSON.stringify(proxy.$store.state));
    });
    
  },
  data(){
    return{
      flag:true
    }
  },
  
}



</script>


<style lang="scss" scoped>
.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}

@import "@/assets/css/var.scss";
@import "@/assets/css/global.scss";


</style>
