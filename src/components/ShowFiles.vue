<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
import { BaseDirectory, FileEntry, readDir } from "@tauri-apps/api/fs";

async function logFiles() {
  var entries = await readDir('/');
  for (const entry of entries) {
    console.log(`Entry: ${entry.path}`);
  }
}

</script>

<template>
  <button @click="logFiles()">Log Files</button>
</template>
