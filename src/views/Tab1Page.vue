<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
            <ion-button>
              <ion-icon :icon="menu"></ion-icon>
            </ion-button>
        </ion-buttons>
        <ion-title>Tab 1</ion-title>
        <ion-buttons slot="end">
          <ion-button id="click-trigger">
            <ion-icon :icon="add"></ion-icon>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
        <ion-item-group>
          <ion-item>Toggle <ion-toggle slot="end"></ion-toggle></ion-item>
          <ion-item>Range <ion-range></ion-range></ion-item>
          <ion-item>
            <ion-select label="Select" placeholder="Favorite Fruit">
              <ion-select-option value="apple">Apple</ion-select-option>
              <ion-select-option value="banana">Banana</ion-select-option>
              <ion-select-option value="orange">Orange</ion-select-option>
            </ion-select>
          </ion-item>
        </ion-item-group>
      </ion-list>
      <div class="ion-padding">
      <ion-button id="open-modal" expand="block">Open Model</ion-button>
    </div>
    </ion-content>

    <ion-popover trigger="click-trigger" trigger-action="click" side="bottom" alignment="center">
      <ion-content class="ion-padding">Popover</ion-content>
    </ion-popover>

   <ion-modal ref="modal" trigger="open-modal" @willDismiss="onWillDismiss">
      <ion-header>
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-button @click="cancel()">Cancel</ion-button>
          </ion-buttons>
          <ion-title>Welcome</ion-title>
          <ion-buttons slot="end">
            <ion-button :strong="true" @click="confirm()">Confirm</ion-button>
          </ion-buttons>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-item>
          <ion-input
            label="Enter your name"
            label-placement="stacked"
            ref="input"
            type="text"
            placeholder="Your name"
          ></ion-input>
        </ion-item>
      </ion-content>
    </ion-modal>


  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonMenuToggle, IonButton, IonButtons, IonPopover, IonToggle, IonRange, IonSelect, IonSelectOption, IonModal, IonInput, IonIcon } from '@ionic/vue';
import { menu, add } from 'ionicons/icons';

  import { OverlayEventDetail } from '@ionic/core/components';
  import { ref } from 'vue';

  const message = ref('This modal example uses triggers to automatically open a modal when the button is clicked.');

  const modal = ref();
  const input = ref();

  const cancel = () => modal.value.$el.dismiss(null, 'cancel');

  const confirm = () => {
    const name = input.value.$el.value;
    modal.value.$el.dismiss(name, 'confirm');
  };

  const onWillDismiss = (event: CustomEvent<OverlayEventDetail>) => {
    if (event.detail.role === 'confirm') {
      message.value = `Hello, ${event.detail.data}!`;
    }
  };
</script>
