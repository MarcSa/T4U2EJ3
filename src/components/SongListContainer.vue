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
    <main>
        <div class="container pb-5">
            <div
                class="d-flex flex-column flex-sm-row justify-content-between align-items-center pb-3"
            >
                <div>
                    <button
                        class="btn mb-2 mb-sm-0"
                        @click="changeFilterState"
                        :class="isFilterActive ? 'active-filter' : ''"
                    >
                        <i class="bi bi-fire me-1" v-if="!isFilterActive"></i>
                        <strong>
                            {{ isFilterActive ? 'Mostrar Todas' : 'Mostrar Éxitos' }}
                        </strong>
                    </button>
                </div>
                <div class="filter-info d-flex justify-content-between mb-2 mb-sm-0">
                    <div
                        class="mostrados d-flex flex-column justify-content-center align-items-center me-3"
                    >
                        <span>{{ displayFilteredSongs().length }}</span>
                        <p class="mb-0">mostrando</p>
                    </div>
                    <div v-once class="d-flex justify-content-center align-items-center">
                        <p class="mb-0 total">Total: {{ songsList.length }}</p>
                    </div>
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
        </div>
    </main>
</template>

<style scoped lang="scss">
$active-color: #f5586c;
main {
    padding-top: 40px;
    background-color: #f8f9fa;
    margin-bottom: 0 !important;
}
.btn {
    background-color: #754ca1;
    color: #ffffff;
    i {
        color: #fa5821;
    }
}
.active-filter {
    background-color: #f5586c;
}
.filter-info {
    color: #6c7480;
    span {
        color: #667de9;
        font-size: 40px;
        font-weight: 700;
        line-height: 45px;
    }
    .mostrados {
        font-size: 16px;
        line-height: 18px;
    }
}
.total {
    font-size: 16px;
    line-height: 18px;
    padding: 10px 15px;
    background-color: #fff !important;
    border: 1px solid #e8ebef;
    border-radius: 0.5em;
}
</style>
