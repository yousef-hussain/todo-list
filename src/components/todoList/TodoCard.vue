<script setup>
import { ref } from "vue";
import ButtonAdd from "./ButtonAdd.vue";

const props = defineProps(["title"]);
const cardData = ref({title: props.title, tasks: []});
const cardsName = {
  buttonShow: 'Add a card',
  buttonAdd: 'Add card'
}

function addInput(val) {
  if (val.length !== 0) {
    cardData.value.tasks.push({ value: val, dialog: false });
  }
}
</script>

<template>
  <v-card class="todo-card-list">
    <v-card-title class="d-flex justify-space-between align-center">
      <input class="title-card text-capitalize fs-14" v-model="cardData.title" />
      <slot name="moreInfo">...</slot>
    </v-card-title>

    <v-card-text class="todo-card-text pb-0">
      <div v-for="(item, index) in cardData.tasks " :key="index">
        <!-- add icon end paragraph -->
        <p class="task text-lowercase fs-14 mb-2">
          {{ item.value }}
          <v-icon class="icon-task" icon="mdi-pencil"></v-icon>
          <v-dialog v-model="item.dialog" activator="parent" width="500">
            <v-card>
              <v-card-text>
                <p>the text is: {{ item.value }}</p>
              </v-card-text>
              <v-card-actions>
                <v-btn color="red" block @click="item.dialog = false">Close Dialog</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </p>
      </div>
    </v-card-text>

    <v-card-actions>
      <ButtonAdd @addItem="addInput" :cardNames="cardsName" />
    </v-card-actions>
  </v-card>
</template>

<style scoped>
.todo-card-list {
  width: 280px;
  margin: 10px;
  border-radius: 15px;
  background-color: #f1f2f4;
  overflow: visible !important;
}
.todo-card-list .title-card {
  resize: none;
  height: 30px;
  min-height: 30px;
  overflow-x: hidden;
  width: 90%;
  padding: 0 8px;
}
.todo-card-list .title-card:focus {
  background-color: #FFF;
  box-shadow: inset 0 0 0 2px #388bff;
}
.todo-card-text {
  max-height: 250px;
  overflow-y: auto;
}
.todo-card-list .task {
  padding: 8px 12px;
  margin: 0;
  background-color: #FFF;
  border-radius: 10px;
  cursor: context-menu;
  box-shadow: 0px 1px 1px #091E4240, 0px 0px 1px #091E424F;
  position: relative;
}
.todo-card-list .task:hover {
  background-color: #f1f2f4;
}
.todo-card-list .task .icon-task {
  position: absolute;
  top: 0px;
  right: 0px;
  font-size: 14px;
  padding: 17px;
  border-radius: 10px;
  color: #44546f;
  visibility: hidden;
}
.todo-card-list .task .icon-task:hover {
  background-color: #dcdfe4;
}
.todo-card-list .task:hover .icon-task {
  visibility: visible;
}
</style>
