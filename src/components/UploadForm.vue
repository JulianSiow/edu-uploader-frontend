<template>
  <div>
    <label
      >Upload your file:
      <input type="file" @change="fileSelected($event)" />
    </label>
    <button type="submit" @click="submitFile">Submit</button>
    <UploadAlertVue
      v-if="showAlert"
      :uploadPercent="uploadPercent"
      :uploadFailed="uploadFailed"
    />
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
import axios from "axios";
import UploadAlertVue from "./UploadAlert.vue";

export default {
  name: "UploadForm",
  components: {
    UploadAlertVue,
  },
  setup() {
    const file = ref<null | File>(null);
    const uploadPercent = ref(0);
    const uploadFailed = ref(false);
    const showAlert = ref(false);

    const fileSelected = (e: Event) => {
      const target = e.target as HTMLInputElement;
      if (target && target.files) {
        file.value = target.files[0];
      }
    };

    const submitFile = () => {
      if (file.value) {
        showAlert.value = true;
        let formData = new FormData();
        formData.append("file", file.value);
        axios
          .post("http://localhost:8080/upload", formData, {
            headers: {
              "Content-Type": "multipart/form-data",
            },
            onUploadProgress: (progressEvent) => {
              uploadPercent.value = Math.round(
                (progressEvent.loaded / progressEvent.total) * 100
              );
            },
          })
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            uploadFailed.value = true;
            console.log(err);
          });
      }
    };

    return {
      file,
      uploadPercent,
      uploadFailed,
      showAlert,
      fileSelected,
      submitFile,
    };
  },
};
</script>

<style></style>
