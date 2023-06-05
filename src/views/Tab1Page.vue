<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-button @click="doShare">SHARE</ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonButton,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import { Share } from "@capacitor/share";

const doShare = async () => {
  const canShareResult = await Share.canShare();
  if (canShareResult.value) {
    const shareResult = await Share.share({
      text: "Text I Am Sharing",
      url: "http://www.clearlyinnovative.com",
    });

    if (shareResult.activityType) {
      alert("Shared to " + shareResult.activityType);
    }
  } else {
    alert(" Cannot Share");
  }
};
</script>
