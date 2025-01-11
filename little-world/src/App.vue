<template>
  <div class="base hello">
    <h1>Hello I'm Min!</h1>
  </div>
  <!-- 其他內容 -->
   <div id = "_2ndpage" class="base" :class="{ visible: is2ndVisible }">
    <h1>以為有什麼嗎？<br>沒有，現在就是啥都還沒有。</h1>
   </div>
   <div id = "_3rdpage" class="base image-container" :class="{ visible: is3rdVisible }" > 
    <h1>只好先放個可愛的尼斯❤︎</h1>
    <img src="/LittleWorld/IMG_5195.jpg" alt="Cute Nency">
   </div>
</template>

<script>
import { onMounted } from 'vue';
export default {
  name: 'App',

  data() {
    return {
      is2ndVisible: false, // 控制是否顯示「第二頁」
      is3rdVisible: false,
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

      const aboutNancySection = document.getElementById("_3rdpage");
      const sectionNancyPosition = aboutNancySection.getBoundingClientRect().top;
      const screenHeight = window.innerHeight;

      if (sectionPosition < screenHeight - 100) {
        this.is2ndVisible = true; // 顯示「第二頁」
      }
      if (sectionNancyPosition < screenHeight - 200) {
        this.is3rdVisible = true; // 顯示「第三頁」
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

#_2ndpage,
#_3rdpage {
  opacity: 0;
}

#_2ndpage.visible,
#_3rdpage.visible {
  opacity: 1;
  animation: fadeIn 2s ease-in-out;
  color: #333;
}

.image-container {
  display: block; 
  justify-content: center; /* 水平置中 */
  align-items: center; /* 垂直置中 */
  height: 100vh; /* 設定容器高度，這裡使用全視窗高度 */
  padding-top: 10vh;
}

.image-container img {
  max-width: 80%; /* 圖片寬度不超過容器的 80% */
  max-height: 80%; 
  height: auto; /* 保持圖片比例 */
  border-radius: 8px; /* （選擇性）設定圖片圓角 */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* （選擇性）增加陰影效果 */
}
</style>