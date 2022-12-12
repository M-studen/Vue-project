<template>
  <el-menu
    :default-active="activeIndex"
    class="el-menu-demo"
    mode="horizontal"
    :ellipsis="false"
    @select="handleSelect">
    <el-menu-item index="0">电脑配件管理</el-menu-item>
    <div class="flex-grow"></div>
    <el-menu-item index="1">
      <el-switch
        v-model="value1"
        class="mt-2"
        style="margin-left: 24px"
        inline-prompt
        :active-icon="MoonNight"
        :inactive-icon="Sunny"
        :active-value="1"
        :inactive-value="0"
        @change="switchThemes" />
    </el-menu-item>
  </el-menu>
</template>

<script lang="ts" setup>
import { MoonNight, Sunny } from "@element-plus/icons-vue";
import { ref } from "vue";
import { useDark, useToggle } from "@vueuse/core";

const activeIndex = ref("1");
const handleSelect = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};
const isDark = useDark();
const switchThemes = () => {
  const toggleDark = useToggle(isDark);
  console.log(toggleDark());
};
let value1 = ref(1);
</script>

<style>
.flex-grow {
  flex-grow: 1;
}
</style>
