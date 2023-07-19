<script setup>
import { defineAsyncComponent, onUpdated, ref, shallowRef, triggerRef } from "vue";
import ButtonAdd from "./todoList/ButtonAdd.vue";
const TodoComp = defineAsyncComponent(() => import("./todoList/TodoCard.vue"));

const cards = shallowRef([]);
const cardsName = {
  buttonShow: "Add another list",
  buttonAdd: "Add list",
};
const moreInfo = ref([
  {
    name: "delete card",
    action: (id) => deleteCard(id),
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
  {
    name: "test",
    action: () => {alert('the function not work')},
  },
]);

function addCard(val, id) {
  if (val.length !== 0) {
    cards.value.push({ id: id, name: TodoComp,  title: val });
    triggerRef(cards);
  }
}
function deleteCard(id) {
  cards.value = cards.value.filter((item) => item.id !== id);
  triggerRef(cards);
}
// to test
onUpdated(() => {
  // console.log(cards.value);
});
</script>

<template>
  <section class="todo-list d-flex justify-start align-start">
    <!-- why the component don't update the DOM -->
    <component
      v-for="(item, index) in cards"
      :key="index"
      :is="item.name"
      :title="item.title"
    >
      <template #moreInfo>
        <v-menu location="end">
          <template v-slot:activator="{ props }">
            <v-btn
              class="more-info pa-0"
              :elevation="0"
              density="compact"
              v-bind="props"
              >...</v-btn
            >
          </template>
          <v-list class="container-lists pa-0" :elevation="0">
              <v-list-item class="list-item pa-0" v-for="list in moreInfo" :key="list.id">
                <v-btn
                  class="text-lowercase fs-14 w-100"
                  @click="list.action(item.id)"
                  :elevation="0"
                  >{{ list.name }}</v-btn
                >
              </v-list-item>
          </v-list>
        </v-menu>
      </template>
    </component>
    <div style="margin: 10px">
      <ButtonAdd @addItem="addCard" :cardNames="cardsName" style="color: #FFF" />
    </div>
  </section>
</template>

<style>
.list-title {
  text-align: center;
  padding: 7px 12px;
}
.more-info ,
.more-info:focus {
  background-color: #f1f2f4 !important;
}
.container-lists {
  width: 250px;
  overflow-y: scroll;
  max-height: 100%;
  background-color: #FFF;
  border-radius: 15px;
}

</style>
