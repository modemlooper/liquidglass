<template>
  <ion-app>
    <ion-split-pane content-id="main-content">

      <ion-menu id="side-menu" content-id="main-content" type="reveal">
        <ion-content>
          <ion-list>
            <ion-item-group>
              <ion-item>Item 1</ion-item>
              <ion-item>Item 2</ion-item>
              <ion-item>Item 3</ion-item>
            </ion-item-group>
          </ion-list>
        </ion-content>
      </ion-menu>

      <ion-router-outlet id="main-content" :animated="false" />
    </ion-split-pane>
  </ion-app>
</template>

<script setup lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
</script>
