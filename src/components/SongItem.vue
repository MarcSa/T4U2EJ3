<script setup lang="ts">
import type { Songs } from '@/interfaces/songs.interface';
const props = defineProps<{ songData: Songs }>();
</script>

<template>
    <section class="card">
        <div class="card-body">
            <div class="header d-flex justify-content-between">
                <h5>
                    <strong>{{ props.songData.title }}</strong>
                </h5>
                <div class="icon-container" v-if="props.songData.isTopHit">
                    <i class="bi bi-fire"></i>
                </div>
            </div>
            <div class="data">
                <div class="artist-data d-flex justify-content-between">
                    <p class="mb-0"><strong>Artista:</strong></p>
                    <p class="mb-0">{{ props.songData.artist }}</p>
                </div>
                <div class="duration-data d-flex justify-content-between">
                    <p class="mb-0"><strong>Duración:</strong></p>
                    <p class="mb-0">{{ props.songData.duration }}</p>
                </div>
                <p class="text-center">
                    {{ props.songData.isTopHit ? 'ÉXITO ACTUAL' : 'CANCIÓN' }}
                </p>
            </div>
        </div>
    </section>
</template>

<style scoped></style>
