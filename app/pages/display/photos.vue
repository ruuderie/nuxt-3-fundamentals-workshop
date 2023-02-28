<script setup>
import { ref } from 'vue'

let photoGallery = ref([])

const route = useRoute()

const filteredPhotoGallery = computed(() => {
  if (route.query.even) {
    return photoGallery.value.filter(photo => photo.albumId % 2 === 0)
  } else {
    return photoGallery.value
  }
})
</script>

<template>
        <Html>
        <Head>
            <Title>Fotos</Title>
            <Link rel="preconnect" href="https://fonts.googleapis.com"/>
<Link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<Link href="https://fonts.googleapis.com/css2?family=Inter:wght@100&display=swap" rel="stylesheet"/>        
</Head>
    </Html>
<NuxtLayout name="photo">
    <div class="section">
        <NuxtPage v-if="route.params.id" />
    <BaseDisplay
        v-else
        title="Photo Gallery"
        itemType="photos"
        v-model:itemList="photoGallery"
    >
        <template v-slot:hero>
        <p>{{ filteredPhotoGallery.length }} photos</p>
        </template>
        <template v-slot:items>
        <li v-for="photo in filteredPhotoGallery" :key="`photo-id-${photo.id}`">
            <NuxtLink :to="`/display/photos/${photo.id}`">
                <img :src="photo.thumbnailUrl"/>        
            </NuxtLink>
        </li>
        </template>
    </BaseDisplay>
    </div>
  </NuxtLayout>
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
