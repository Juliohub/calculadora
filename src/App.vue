<template>
  <div id="app">
    <ContentCalculator />
  </div>
</template>

<script>
import ContentCalculator from "@/components/ContentCalculator.vue";

export default {
  name: "App",
  components: {
    ContentCalculator,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Grandstander:wght@300;400;700&display=swap");
:root {
  --primary-color: #212121;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body,
button {
  font-family: "Grandstander", cursive;
  font-size: 1rem;
  color: #fff;
}
</style>
