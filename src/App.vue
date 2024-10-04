<script setup>
import { ref } from 'vue';

const msg = ref('Shopping list App');

const text = ref('');
const newItemPriorityRadio = ref('low');
const newItemPrioritySelect = ref('low');
const newItemPriorityCheck = ref(false);
const iceCreamFlavors = ref(['chocolate']);

const editing = ref(false);
const items = ref([
  // { id: 1, label: '10 party hats' },
  // { id: 2, label: '2 board games' },
  // { id: 3, label: '20 cups' },
]);
const newItem = ref('');

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });
  newItem.value = '';
};

const doEdit = (e) => {
  editing.value = e;
  newItem.value = '';
};
</script>

<template>
  <main>
    <h1>{{ msg }}</h1>
    <input v-model.trim="text" type="text" placeholder="Add text" />
    <br />
    <br />
    value: {{ text }}

    <hr />

    Priority Radio:
    <label>
      <input type="radio" v-model="newItemPriorityRadio" value="low" />Low
    </label>
    <label>
      <input type="radio" v-model="newItemPriorityRadio" value="high" />High
    </label>
    <br />
    <br />
    value: {{ newItemPriorityRadio }}

    <hr />

    <label for="">
      Priority Select:
      <select v-model="newItemPrioritySelect">
        <option value="low">Low</option>
        <option value="high">High</option>
      </select>
    </label>
    <br />
    <br />
    value: {{ newItemPrioritySelect }}

    <hr />

    <label for="">
      <input type="checkbox" v-model="newItemPriorityCheck" />
      High Priority
    </label>
    <br />
    <br />
    value: {{ newItemPriorityCheck }}

    <hr />

    <label for="">
      <input type="checkbox" value="vanilla" v-model="iceCreamFlavors" />Vanilla
    </label>
    <label for="">
      <input
        type="checkbox"
        value="chocolate"
        v-model="iceCreamFlavors"
      />Chocolate
    </label>
    <label for="">
      <input
        type="checkbox"
        value="strawberry"
        v-model="iceCreamFlavors"
      />Strawberry
    </label>
    <br />
    <br />
    value: {{ iceCreamFlavors }}

    <hr />

    <label for="">
      <input type="checkbox" v-model="editing" />
      Form Add - {{ editing }}
    </label>
    <br />
    <br />
    <button v-if="editing" @click="doEdit(false)">Cancel</button>
    <button v-else @click="doEdit(true)">Add Form</button>
    <br />
    <br />

    <form v-if="editing" @submit.prevent="saveItem">
      Add Items:
      <input v-model.trim="newItem" type="text" placeholder="Add a new item" />
      <button>Add a New Item</button>

      <ul>
        <li v-for="({ id, label }, index) in items" :key="id">
          {{ label }}
        </li>
      </ul>

      <p v-if="!items.length">Nothing to see here!</p>
    </form>
  </main>
</template>

<style scoped></style>
