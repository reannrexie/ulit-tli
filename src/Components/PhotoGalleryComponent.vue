<template>
  <ion-card class="gallery-card">
    <ion-card-header>
      <div class="gallery-icon-wrapper">
        <ion-icon :icon="imagesIcon" />
      </div>

```
  <ion-card-title>Photo Gallery</ion-card-title>
  <ion-card-subtitle>
    Your captured photos
  </ion-card-subtitle>
</ion-card-header>

<ion-card-content>
  <!-- Empty Gallery -->
  <div
    v-if="photos.length === 0"
    class="empty-gallery"
  >
    <div class="empty-icon">
      <ion-icon :icon="imageOutline" />
    </div>

    <h3>No pictures yet</h3>

    <p>
      Take a picture using the camera
      and it will appear here.
    </p>
  </div>

  <!-- Photos -->
  <ion-grid v-else class="photo-grid">
    <ion-row>
      <ion-col
        v-for="(photo, index) in photos"
        :key="index"
        size="6"
        size-md="4"
      >
        <div class="photo-item">
          <ion-img
            :src="photo"
            class="gallery-image"
          />

          <div class="photo-number">
            {{ index + 1 }}
          </div>
        </div>
      </ion-col>
    </ion-row>
  </ion-grid>
</ion-card-content>
```

  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonImg,
  IonIcon,
} from "@ionic/vue";

import {
  imagesOutline as imagesIcon,
  imageOutline,
} from "ionicons/icons";

defineProps<{
  photos: string[];
}>();
</script>

<style scoped>
/* Main Gallery Card */
.gallery-card {
  margin: 0 0 20px;
  border: 1px solid #d7e3ec;
  border-radius: 20px;
  background: #ffffff;
  box-shadow: 0 6px 20px rgba(62, 105, 133, 0.10);
  overflow: hidden;
}

/* Header */
ion-card-header {
  text-align: center;
  padding: 24px 20px 12px;
}

.gallery-icon-wrapper {
  width: 58px;
  height: 58px;
  margin: 0 auto 12px;
  border-radius: 16px;
  background: #e8f1f7;
  display: flex;
  align-items: center;
  justify-content: center;
}

.gallery-icon-wrapper ion-icon {
  font-size: 28px;
  color: #3e6985;
}

ion-card-title {
  font-size: 22px;
  font-weight: 700;
  color: #0d273d;
}

ion-card-subtitle {
  margin-top: 6px;
  color: #718494;
  font-size: 14px;
}

/* Gallery Content */
ion-card-content {
  padding: 16px 20px 24px;
}

/* Empty Gallery */
.empty-gallery {
  padding: 35px 20px;
  text-align: center;
}

.empty-icon {
  width: 70px;
  height: 70px;
  margin: 0 auto 16px;
  border-radius: 20px;
  background: #f0f5f8;
  display: flex;
  align-items: center;
  justify-content: center;
}

.empty-icon ion-icon {
  font-size: 34px;
  color: #8aa7bc;
}

.empty-gallery h3 {
  margin: 0 0 8px;
  color: #0d273d;
  font-size: 18px;
  font-weight: 700;
}

.empty-gallery p {
  max-width: 280px;
  margin: 0 auto;
  color: #718494;
  font-size: 14px;
  line-height: 1.6;
}

/* Photo Grid */
.photo-grid {
  padding: 0;
}

.photo-grid ion-row {
  margin: -6px;
}

/* Individual Photo */
.photo-grid ion-col {
  padding: 6px;
}

.photo-item {
  position: relative;
  overflow: hidden;
  border-radius: 14px;
  border: 1px solid #d7e3ec;
  background: #f5f8fa;
  box-shadow: 0 4px 12px rgba(62, 105, 133, 0.08);
}

/* Image */
.gallery-image {
  width: 100%;
  height: 180px;
  display: block;
}

.gallery-image::part(image) {
  object-fit: cover;
}

/* Photo Number */
.photo-number {
  position: absolute;
  top: 8px;
  right: 8px;

  min-width: 28px;
  height: 28px;

  padding: 0 7px;

  border-radius: 9px;
  background: rgba(13, 39, 61, 0.78);
  color: #ffffff;

  display: flex;
  align-items: center;
  justify-content: center;

  font-size: 12px;
  font-weight: 600;
}

/* Mobile */
@media (max-width: 576px) {
  .gallery-image {
    height: 150px;
  }

  ion-card-header {
    padding-top: 20px;
  }

  .gallery-icon-wrapper {
    width: 52px;
    height: 52px;
  }

  .gallery-icon-wrapper ion-icon {
    font-size: 25px;
  }
}
</style>
