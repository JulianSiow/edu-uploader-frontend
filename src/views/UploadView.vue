<template>
  <div>
    <h1>Upload</h1>
    <UploadForm></UploadForm>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import UploadForm from "@/components/UploadForm.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    UploadForm,
  },
});
</script>
