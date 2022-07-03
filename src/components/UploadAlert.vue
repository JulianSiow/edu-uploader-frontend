<template>
  <div>
    <div v-if="uploadPercent && uploadPercent > 100">Uploading...</div>
    <div v-if="uploadPercent && uploadPercent <= 100 && !uploadFailed">
      Upload Succeeded!
    </div>
    <div v-if="uploadFailed">Upload Failed...</div>
    <progress max="100" :value="uploadPercent"></progress>
  </div>
</template>

<script lang="ts">
import { toRefs, defineComponent } from "vue";

export default defineComponent({
  props: {
    uploadPercent: Number,
    uploadFailed: Boolean,
  },
  setup(props) {
    const { uploadPercent, uploadFailed } = toRefs(props);
  },
});
</script>

<style></style>
