<script setup>
import { ref, onMounted, computed } from "vue";
import axios from "axios";

const surahs = ref(null);

const fetchSurah = async () => {
  try {
    const response = await axios.get(`http://api.alquran.cloud/v1/surah`);
    surahs.value = response.data.data;
  } catch (error) {
    console.error(error);
  }
};

onMounted(() => {
  fetchSurah();
});
</script>
<template>
  <div>
    <h2>Surahs</h2>
    <div v-for="surah in surahs" :key="surah.number" class="py-4 flex flex-col">
      <div class="flex gap-2 text-xl">
        <h3>{{ surah.englishName }}</h3>
        <h3>{{ surah.name }}</h3>
      </div>
      <div class="flex gap-2 items-center">
        <span> {{ surah.englishNameTranslation }} | </span>
        <span class="text-sm"> {{ surah.revelationType }}</span>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
