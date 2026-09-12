<template>
  <ion-page>
    <ion-header class="custom-header">
      <ion-toolbar>
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

```
<ion-content class="gallery-page">
  <div class="page-container">

    <!-- Welcome Section -->
    <div class="welcome-section">
      <div class="welcome-icon">
        <ion-icon :icon="imagesIcon" />
      </div>

      <div>
        <h1>My Photo Gallery</h1>
        <p>Capture and keep your favorite moments.</p>
      </div>
    </div>

    <!-- Camera -->
    <CameraComponent
      @photo-captured="addPhoto"
    />

    <!-- Photo Gallery -->
    <PhotoGalleryComponent
      :photos="photos"
    />

  </div>
</ion-content>
```

  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonIcon,
} from "@ionic/vue";

import { ref } from "vue";

import { imagesOutline as imagesIcon } from "ionicons/icons";

import CameraComponent from "../Components/CameraComponent.vue";
import PhotoGalleryComponent from "../Components/PhotoGalleryComponent.vue";

const photos = ref<string[]>([]);

const addPhoto = (photo: string) => {
  photos.value.unshift(photo);
};
</script>

<style scoped>
/* Header */
.custom-header ion-toolbar {
  --background: #ffffff;
  --color: #0d273d;

  border-bottom: 1px solid #d7e3ec;
  box-shadow: 0 2px 10px rgba(62, 105, 133, 0.06);
}

.custom-header ion-title {
  font-size: 19px;
  font-weight: 700;
  letter-spacing: 0.2px;
}

/* Page */
.gallery-page {
  --background: #f4f8fb;
}

.page-container {
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

/* Welcome Section */
.welcome-section {
  display: flex;
  align-items: center;
  gap: 15px;

  margin-bottom: 20px;
  padding: 20px;

  background: #ffffff;
  border: 1px solid #d7e3ec;
  border-radius: 18px;

  box-shadow: 0 5px 16px rgba(62, 105, 133, 0.07);
}

.welcome-icon {
  flex-shrink: 0;

  width: 52px;
  height: 52px;

  border-radius: 15px;

  background: #e8f1f7;

  display: flex;
  align-items: center;
  justify-content: center;
}

.welcome-icon ion-icon {
  font-size: 27px;
  color: #3e6985;
}

/* Welcome Text */
.welcome-section h1 {
  margin: 0;

  color: #0d273d;

  font-size: 21px;
  font-weight: 700;
}

.welcome-section p {
  margin: 5px 0 0;

  color: #718494;

  font-size: 13px;
  line-height: 1.5;
}

/* Mobile */
@media (max-width: 576px) {
  .page-container {
    padding: 14px;
  }

  .welcome-section {
    padding: 16px;
    gap: 12px;
  }

  .welcome-icon {
    width: 46px;
    height: 46px;
    border-radius: 13px;
  }

  .welcome-icon ion-icon {
    font-size: 24px;
  }

  .welcome-section h1 {
    font-size: 18px;
  }

  .welcome-section p {
    font-size: 12px;
  }
}
</style>
