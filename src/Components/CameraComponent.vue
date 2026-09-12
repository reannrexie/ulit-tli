<template>   <ion-card class="camera-card">     <ion-card-header>       <div class="camera-icon-wrapper">         <ion-icon :icon="cameraIcon" />       </div>

```
  <ion-card-title>Camera</ion-card-title>
  <ion-card-subtitle>
    Capture a photo for your gallery
  </ion-card-subtitle>
</ion-card-header>

<ion-card-content>
  <ion-button
    expand="block"
    class="take-photo-button"
    @click="takePicture"
  >
    <ion-icon slot="start" :icon="cameraIcon" />
    Take Picture
  </ion-button>

  <ion-text v-if="errorMessage" class="error-message">
    <p>{{ errorMessage }}</p>
  </ion-text>
</ion-card-content>
```

  </ion-card> </template>

<script setup lang="ts">
import {
  IonButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonIcon,
  IonText,
} from "@ionic/vue";

import { camera as cameraIcon } from "ionicons/icons";
import { Camera } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");

const emit = defineEmits<{
  (event: "photoCaptured", photo: string): void;
}>();

const takePicture = async () => {
  errorMessage.value = "";

  try {
    const photo = await Camera.takePhoto({
      quality: 90,
      saveToGallery: false,
    });

    if (photo.webPath) {
      emit("photoCaptured", photo.webPath);
    }
  } catch (error) {
    console.error(error);

    errorMessage.value =
      "Unable to capture photo. Please check your camera permissions.";
  }
};
</script>

<style scoped>
.camera-card {
  margin: 16px 0 24px;
  border: 1px solid #d7e3ec;
  border-radius: 20px;
  background: #ffffff;
  box-shadow: 0 6px 20px rgba(62, 105, 133, 0.10);
  overflow: hidden;
}

ion-card-header {
  text-align: center;
  padding: 24px 20px 12px;
}

.camera-icon-wrapper {
  width: 58px;
  height: 58px;
  margin: 0 auto 12px;
  border-radius: 16px;
  background: #e8f1f7;
  display: flex;
  align-items: center;
  justify-content: center;
}

.camera-icon-wrapper ion-icon {
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

ion-card-content {
  padding: 16px 20px 24px;
}

.take-photo-button {
  --background: #3e6985;
  --background-hover: #315a75;
  --background-activated: #294f68;
  --color: #ffffff;
  --border-radius: 13px;
  --box-shadow: 0 5px 12px rgba(62, 105, 133, 0.20);

  height: 50px;
  font-size: 15px;
  font-weight: 600;
  text-transform: none;
  letter-spacing: 0.2px;
}

.take-photo-button ion-icon {
  font-size: 20px;
}

.error-message {
  display: block;
  margin-top: 14px;
  padding: 10px 12px;
  border-radius: 10px;
  background: #fff1f1;
  color: #c0392b;
  font-size: 13px;
  text-align: center;
}

.error-message p {
  margin: 0;
}
</style>
