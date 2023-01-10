<template>
  <div class="home">
    <MyIndex />
  </div>
</template>

<script>
// @ is an alias to /src
import MyIndex from "@/components/MyIndex.vue";

export default {
  name: "HomeView",
  components: {
    MyIndex,
  },
};
</script>
