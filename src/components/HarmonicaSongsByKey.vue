<template>
  <div>
    <select v-model="selectedKey" @change="fetchSongs">
      <option disabled value="">Please select a key</option>
      <option>A</option>
      <option>C</option>
      <option>G</option>
      <!-- Add other keys here -->
    </select>

    <ul>
      <li style="list-style-type:none;" v-for="song in songs" :key="song"><a :href="song">{{ song }}</a></li>
    </ul>
  </div>
</template>

<script lang="ts">
import { ref, Ref } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const selectedKey: Ref<string> = ref('');
    const songs: Ref<string[]> = ref([]);

    const fetchSongs = async () => {
      if (selectedKey.value) {
        const response = await axios.get(`http://localhost:5217/Harmonicas/${selectedKey.value}`);
        songs.value = response.data;
      }
    };

    return { selectedKey, songs, fetchSongs };
  },
};
</script>