<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
import { BaseDirectory, FileEntry, readDir } from "@tauri-apps/api/fs";

var entries: FileEntry[];
var dir = ref('/');
// FileEntry -> { path: string, name: string? children: string?[]}

async function logFiles() {
  entries = await readDir(dir.value);
  for (const object of entries) {
    console.log(`Entry: ${object.path}`);
  }
}

function clear() {
  entries = [];
}

function setDir(entry:FileEntry){
  dir.value = entry.path;
}

</script>

<template>
  <button @click="clear()">Clear Folder</button>
  <button @click="logFiles()">Log Files</button>
  <div class="v-list" v-for="(entry, index) in entries" @click="setDir(entry)">
    {{ entry.path }}
  </div>
</template>
