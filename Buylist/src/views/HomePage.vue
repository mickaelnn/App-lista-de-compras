<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Buylist</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Buylist</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-item>
          <ion-input type="text" v-model="state.input" placeholder="ITEM A ADICIONAR"></ion-input>
          <ion-button @click="addCartProduct">Adicionar</ion-button>
        </ion-item>
        <ion-list>
          <ion-item v-for="(item, index) in state.cart" :key="index">
            <ion-label>{{item}}</ion-label>
            <ion-button @click="removeCartProduct(index)">Remover</ion-button>
          </ion-item>
        </ion-list>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts" setup>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonInput, IonItem, IonButton, IonList, IonLabel, alertController, toastController   } from '@ionic/vue';
import { ref } from 'vue';


const state = ref<{ input: string, cart: Array<string> }>({
  input: '',
  cart: [],
});

const openToast = async (msg: string) => {
  const toast = await toastController.create({
    message: msg,
    duration: 2000,
  })
  toast.present();
};

const addCartProduct = async () => {
const alert = await alertController.create({
  header: 'Sem produto',
  message: 'Você precisa adicionar um produto',
});

  const item = state.value.input;
  if (!item) {
    alert.present();
    return;
  }

  state.value.cart.push(item);
  openToast('Produto adicionado');
  state.value.input = '';
};

const removeCartProduct = (index: number) => {
  state.value.cart.splice(index, 1);
  openToast('Produto excluido');
}

</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
