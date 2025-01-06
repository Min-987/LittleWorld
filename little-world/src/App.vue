<template>
  <div class="base hello">
    <h1>Hello I'm Min!</h1>
  </div>
  <!-- 其他內容 -->
   <div id = "_2ndpage"  class="base"  :class="{ visible: is2ndVisible }">
    <h1>以為有什麼嗎？<br>沒有，現在就是啥都還沒有。<br>嘿嘿...555</h1>
   </div>
</template>

<script>
import { onMounted } from 'vue';
export default {
  name: 'App',

  data() {
    return {
      is2ndVisible: false, // 控制是否顯示「第二頁」
    };
  },
  setup() {
    onMounted(() => {
      window.scrollTo(0, 0);
    });
  },
  methods: {
    handleScroll() {
      const aboutMeSection = document.getElementById("_2ndpage");
      const sectionPosition = aboutMeSection.getBoundingClientRect().top;
      const screenHeight = window.innerHeight;

      if (sectionPosition < screenHeight - 100) {
        this.is2ndVisible = true; // 顯示「第二頁」
        window.removeEventListener("scroll", this.handleScroll); // 停止監聽
      }
    },
  },
  mounted() {
    window.scrollTo(0, 0); // 滾動到頂部
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },

};
</script>

<style>
.base {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-align: center;
  font-family: Arial, sans-serif;
  font-size: 2rem;
  background-color: #f9f9f9;
}

@keyframes fadeIn {
  from { opacity: 0; } /* 開始透明 */
  to { opacity: 1; }   /* 最終可見 */
}

.hello h1 {
  animation: fadeIn 2s ease-in-out; /* 套用動畫 */
  color: #333;
}

#_2ndpage {
  opacity: 0;
}

#_2ndpage.visible {
  opacity: 1;
  animation: fadeIn 2s ease-in-out;
  color: #333;
}
</style>