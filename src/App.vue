<template>
  <div id="app">
    <div id="nav">
      {{ name }}----{{ age }}---{{ count }}----{{ store.state.countNum }}
      <input v-model="store.state.countNum" type="number" />
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
      <router-link to="/test">Test</router-link>
      <button @click="add">点我+1</button>
    </div>
    <router-view />
    <!-- <HelloWorld /> -->
  </div>
</template>

<script>
import { reactive, ref, onMounted, onUpdated, onUnmounted, toRefs } from "vue";
import { getCurrentInstance } from "vue";
import { useStore } from "vuex";
// import HelloWorld from "@/components/HelloWorld";
// import { useRouter } from "vue-router";
export default {
  // components: {
  //   HelloWorld
  // },
  setup() {
    const store = useStore();
    onMounted(() => {
      console.log("mounted!");
      console.log(store.state);
    });
    onUpdated(() => {
      console.log("updated!");
    });
    onUnmounted(() => {
      console.log("unmounted!");
    });

    // const Router = useRouter();
    // const Route = useRoute();
    const { ctx } = getCurrentInstance();
    // console.log(ctx);
    const info = reactive({
      name: "yangyaun",
      age: 18,
      sex: 1
    });
    console.log("我是setup");
    const count = ref(0);
    const add = () => {
      count.value += 1;
      info.age += 1;
      store.state.countNum += 1;
      // Router.push("/test");
      ctx.$router.push("/test");
    };
    console.log(count.value);

    return { ...toRefs(info), add, count, store };
  }
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
