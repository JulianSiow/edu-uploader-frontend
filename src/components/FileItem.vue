<template>
  <li>{{ fileName }}</li>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    fileName: String,
  },
});
</script>

<style></style>
