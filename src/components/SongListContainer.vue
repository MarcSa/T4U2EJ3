<script setup lang="ts">
import { ref } from 'vue';
import type { Songs } from '@/interfaces/songs.interface';
import SongItem from '@/components/SongItem.vue';
import json from '@/data/songs.json';

const songsList: Songs[] = json;
const isFilterActive = ref<boolean>(false);
const changeFilterState = () => {
    isFilterActive.value = !isFilterActive.value;
};
const displayFilteredSongs = () => {
    return songsList.filter((song) => song.isTopHit || !isFilterActive.value);
};
</script>

<template>
    <main class="container">
        <div class="">
            <div>
                <button class="btn" @click="changeFilterState">
                    <i class="bi bi-fire" v-if="!isFilterActive"></i>
                    {{ isFilterActive ? 'Mostrar Todas' : 'Mostrar Éxitos' }}
                </button>
            </div>
            <div class="filter-info">
                <div class="mostrados">
                    <span>{{ displayFilteredSongs().length }}</span>
                    <p>mostrando</p>
                </div>
                <div v-once class="total">Total: {{ songsList.length }}</div>
            </div>
        </div>
        <div class="row">
            <div
                class="col-12 col-md-4 mb-4"
                v-for="songEl in displayFilteredSongs()"
                :key="songEl.id"
            >
                <SongItem :songData="songEl" />
            </div>
        </div>
    </main>
</template>

<style scoped></style>
