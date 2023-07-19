<script setup>
import { ref } from 'vue';
const props = defineProps(['cardNames']);
const emit = defineEmits(['addItem',]);

const toggleSwitch = ref(true)
const textInput = ref('');
const id = ref(0);
const expand = ref(false);

function checkInput() {
  if(textInput.value !== 0 ) {
    emit('addItem', textInput.value, id.value++);
    textInput.value = '';
  }
}

function addNewItem() {
  checkInput();
}

function closeForm () {
  checkInput();
  toggleSwitch.value = true;
}
</script>

<template>
  <div class="button-add-item">
      <v-btn v-if="toggleSwitch" class="btn-add-list d-flex justify-start text-capitalize fs-14" :style="$attrs.style" @click="toggleSwitch = false;" prepend-icon="mdi-plus" elevation="0" >{{ props.cardNames.buttonShow }}</v-btn>
      
      <v-form v-else class="form-data" @submit.prevent>
        <v-text-field class="input-text fs-14 mb-5"  v-model="textInput" placeholder="Enter List Title" density="compact" autofocus hide-details @keyup.enter="addNewItem()" ></v-text-field>
        <v-btn class="btn-add text-capitalize fs-14 px-5 py-3 mr-3" @click="addNewItem()">{{ props.cardNames.buttonAdd }}</v-btn>
        <v-btn class="btn-close fs-14 " @click="closeForm" prepend-icon="mdi-close" :elevation="0"></v-btn>
      </v-form>
    </div>
</template>


<style scoped>
.button-add-item .btn-add-list {
  width: 250px; 
  background-color: #ffffff3d;
  border-radius: 12px;
}
.form-data {
  background-color: #f1f2f4;
  border-radius: 10px;
  padding: 10px;
  width: 260px; 
  display: block;
}
.form-data .input-text {
  box-shadow: inset 0 0 0 2px #388bff;
  background-color: #FFF;
  color: #000;
}
.form-data .btn-add {
  background-color: #08479E;
  color: white;
}
.form-data .btn-close {
  background-color: #f1f2f4;
}
</style>