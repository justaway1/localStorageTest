<script setup>
import { ref, onMounted } from "vue";

const text = ref("Edit me");
const checked = ref(true);
const checkedNames = ref(["Jack"]);
const picked = ref("One");
const select = ref("A");
const multiSelect = ref(["A"]);

const savedState = () => {
  const formData = {
    text: text.value,
    checked: checked.value.value,
    checkedNames: checkedNames.value,
    picked: picked.value,
    select: select.value,
    multiSelect: multiSelect.value,
  };

  const savedData = JSON.parse(localStorage.getItem("formData"));
  const updatedData = { ...savedData, ...formData };

  localStorage.setItem("formData", JSON.stringify(updatedData));
};

onMounted(() => {
  const getData = JSON.parse(localStorage.getItem("formData"));

  text.value = getData.text || "";
  checked.value = getData.checked || "";
  checkedNames.value = getData.checkedNames || "";
  picked.value = getData.picked || "";
  select.value = getData.select || "";
  multiSelect.value = getData.multiSelect || "";
});
</script>

<template>
  <div>
    <form class="form">
      <H2>Text Input</H2>
      <input v-model="text" type="text" id="text" />
      <label for="text">{{ text }}</label>

      <h2>Checkboxes</h2>
      <input type="checkbox" v-model="checked" id="checked" />
      <label for="checked">Checked: {{ checked }}</label>

      <h2>Multiple Checkboxes</h2>
      <input type="checkbox" v-model="checkedNames" id="Jack" value="Jack" />
      <label for="Jack">Jack</label>
      <input type="checkbox" v-model="checkedNames" id="John" value="John" />
      <label for="John">John</label>
      <input type="checkbox" v-model="checkedNames" id="Mary" value="Mary" />
      <label for="Mary">Mary</label>
      <br />
      <br />
      <span>
        Checked names:
        <pre>{{ checkedNames }}</pre>
      </span>
      <h2>Radio</h2>
      <input type="radio" name="radio" id="one" value="One" v-model="picked" />
      <label for="one">One</label>
      <input type="radio" name="radio" id="two" value="Two" v-model="picked" />
      <label for="two">Two</label>
      <br />
      <br />
      <span>Picked: {{ picked }}</span>

      <h2>Select</h2>
      <select v-model="select">
        <option disabled>Please select one</option>
        <option value="A">A</option>
        <option value="B">B</option>
        <option value="C">C</option>
      </select>
      <span>Selected: {{ select }}</span>

      <h2>Multiple selection</h2>
      <select v-model="multiSelect" multiple>
        <option disabled value>Please select more than one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
      <span>Multiple Selected: {{ multiSelect }}</span>
      <br />
      <br />

      <button @click.prevent="savedState">Save Your Data</button>
    </form>
  </div>
</template>

<style scoped>
.form {
  background-color: rgb(6, 87, 87);
  color: white;
  padding: 20px;
}
</style>
