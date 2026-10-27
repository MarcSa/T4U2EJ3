<script setup lang="ts">
import type { Songs } from '@/interfaces/songs.interface';
const props = defineProps<{ songData: Songs }>();
</script>

<template>
    <section class="card h-100" :class="props.songData.isTopHit ? 'hit' : ''">
        <div class="card-body d-flex flex-column">
            <div class="text-container flex-grow-1">
                <div class="header d-flex justify-content-between align-items-center mb-3">
                    <h5 class="mb-0">
                        <strong>{{ props.songData.title }}</strong>
                    </h5>
                    <div class="icon-container" v-if="props.songData.isTopHit">
                        <i class="bi bi-fire"></i>
                    </div>
                </div>
                <div class="data">
                    <div class="artist-data d-flex justify-content-between">
                        <p class="mb-0"><strong>Artista:</strong></p>
                        <p class="mb-0 black-text">{{ props.songData.artist }}</p>
                    </div>
                    <hr />
                    <div class="duration-data d-flex justify-content-between mb-4">
                        <p class="mb-0"><strong>Duración:</strong></p>
                        <p class="mb-0 black-text">{{ props.songData.duration }}</p>
                    </div>
                </div>
            </div>
            <p class="text-center mb-2">
                <span> {{ props.songData.isTopHit ? 'ÉXITO ACTUAL' : 'CANCIÓN' }}</span>
            </p>
        </div>
    </section>
</template>

<style scoped lang="scss">
$active-color: #f5586c;
h5 {
    line-height: 25px;
}
.card {
    border-width: 2px;
    border-style: solid;
    border-color: #fff;
    box-shadow: 0px 0px 6px 2px #e9e9e9;
}
.card-body {
    p {
        color: #6c7480;
    }
    .black-text {
        color: #000000;
    }
    margin-top: 2px;
    background-color: #fff;
    border-end-start-radius: 4px;
    border-end-end-radius: 4px;
}
span {
    display: inline-block;
    line-height: 18px;
    padding: 5px 20px;
    border-radius: 14px;
    background-color: #e8ebef;
    font-weight: bold;
}
hr {
    margin: 6px 0;
    border-color: #f1f3f4;
}
.hit {
    border: 2px solid $active-color;
    background-color: $active-color;
    .card-body {
        background-color: #fffbfb;
    }
    span {
        background-color: #ff8787;
        color: #fff;
    }
    i {
        color: $active-color;
        font-size: 30px;
    }
}
</style>
