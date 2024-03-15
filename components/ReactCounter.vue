<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useState } from "react";
import ReactDOM from "react-dom/client";
import { jsxs, jsx } from "react/jsx-runtime";

const root = ref(null)

function App() {
  const [count, setCount] = useState(0);

  return count === 5
    ? jsx("div", { children: "Maximum Reach" })
    : jsxs("div", {
        onClick: () => setCount(count + 1),
        children: ["Count: ", count.toFixed(2)]
      });
}

onMounted(() => {
  console.log(root.value);
  if (root.value) {
    console.log("ROOT VALUe")
   ReactDOM.createRoot(root.value).render(jsx(App, {}))
  //  .render(jsxs(App));
  }
});
</script>

<template>
  <div ref="root" id="react-app"></div>
</template>
