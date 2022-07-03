<template>
  <div>
    <h1>Files</h1>
    <ul>
      <FileItem v-for="file in files" :key="file" :fileName="file" />
    </ul>
  </div>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import FileItem from "@/components/FileItem.vue";

export default {
  components: {
    FileItem,
  },

  setup() {
    const files = ref(null);

    const getFiles = () => {
      axios
        .get("http://localhost:8080/files")
        .then((res) => {
          files.value = res.data.data;
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      getFiles();
    });

    return {
      files,
      getFiles,
    };
  },
};
</script>

<style></style>
