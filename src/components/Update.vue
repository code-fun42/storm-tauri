<script lang="ts">
import {defineComponent} from 'vue'
import {checkUpdate, installUpdate} from "@tauri-apps/api/updater";
// import {checkUpdate, installUpdate} from "@tauri-apps/api/updater";

export default defineComponent({
  name: "Update",
  data() {
    return {
      status: "none"
    };
  },
  methods: {
    async _update() {
      console.log("checkUpdate")
      try {
        const update = await checkUpdate();
        if (update.shouldUpdate) {
          console.log(`Installing update ${update.manifest?.version}, ${update.manifest?.date}, ${update.manifest?.body}`);
          this.status = "Install";
          await installUpdate();
        }

      } catch (err: any) {
        console.log("err: ", err);

        this.status = err;
      }
    }
  },
  created() {
    this._update();
  }
})
</script>

<template>
<div class="">
  <h2>Status: {{ status }}</h2>
</div>
</template>

<style scoped>

</style>