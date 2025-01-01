<template>
  <div class="hello">
    <h1>Hello I'm Min!</h1>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
.hello {
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
</style>