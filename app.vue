<template>
  <div :class="classes">
    <form @submit.prevent="download">
      <div>
        <label for="">Date to generate from</label>
        <Datepicker v-model="today" />
      </div>
      <div>
        <label for="">Format</label>
        <select v-model="format">
          <option v-for="format in formats" :value="format">
            {{ format }}
          </option>
        </select>
      </div>
      <div>
        <label for="">Where</label>
        <input type="text" v-model="where" />
      </div>
      <div>
        <label for="">Edition</label>
        <input type="number" v-model="edition" />
      </div>
      <div>
        <label for="">When</label>
        <Datepicker
          v-model="when"
          inputFormat="yyyy-MM-dd HH:mm"
          minimumView="time"
        />
        {{ when }}
      </div>
      <div>
        <label for="">Image</label>
        <div class="image-preview">
          <img :src="image" class="image-preview" />
          <input type="file" required @change="addFile" />
        </div>
        <div>
          <label for="">Focus</label>

          <input type="range" min="0" max="100" v-model="focus[0]" />
          <input type="range" min="0" max="100" v-model="focus[1]" />
        </div>
        <div>
          <label for="">Author</label>
          <input type="text" required v-model="author" /><br />
        </div>
      </div>
      <div>
        <label for="">Options</label>
        <div>
          <Multiselect
            v-model="classes"
            mode="tags"
            :options="[
              'margin',
              'contain',
              'invert',
              'grey',
              'color',
              'bg',
              'none',
            ]"
          ></Multiselect>
        </div>
        <!-- <select v-model="classes" multiple required size="10">
          <option
            v-for="cls in [
              'invert',
              'grey',
              'color',
              'bg',
              'none',
              'margin',
              'contain',
            ]"
            :value="cls"
          >
            {{ cls }}
          </option>
        </select> -->
      </div>
      <button>Download</button>
    </form>
    <div class="preview">
      <div>
        <label for="">Twitter/Meetup</label>
        <div ref="meetup">
          <Card :data="data" class="main"></Card>
        </div>
      </div>
      <div>
        <label for="">Instagram Story</label>
        <div ref="insta">
          <Card :data="data" class="story"></Card>
        </div>
      </div>
      <div>
        <label for="">Instagram Post / Square</label>
        <div ref="square">
          <Card :data="data" class="square"></Card>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Datepicker from "vue3-datepicker";
import Multiselect from "@vueform/multiselect";
import DefaultImage from "~/assets/default_image";
import {
  isBefore,
  addMonths,
  startOfMonth,
  nextSaturday,
  nextFriday,
} from "date-fns";
import domtoimage from "dom-to-image";
const meetup = ref(null);
const insta = ref(null);
const square = ref(null);

const today = ref(new Date());
const formats = ["Stammtisch", "Jam"];
const format = ref(formats[0]);
const when = ref(new Date());
const edition = ref(103);
const where = ref("co.up Berlin");
const image = ref(DefaultImage);
const author = ref(null);
const classes = ref(null);
const focus = ref([50, 50]);

const data = ref({
  today,
  format,
  edition,
  when,
  where,
  image,
  author,
  focus,
});

useHead({
  link: [
    {
      rel: "preconnect",
      href: "https://fonts.googleapis.com",
    },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Comfortaa&display=swap",
      crossorigin: "",
    },
  ],
});

function addFile(event) {
  let file = event.target.files[0];
  var reader = new FileReader();
  reader.readAsDataURL(file);
  reader.onload = function () {
    image.value = reader.result;
  };
}
function generateNextEvent() {
  let stammtisch = {
    edition: 102,
    date: new Date(2022, 9, 7, 19, 30),
    type: formats[0],
  };
  while (isBefore(stammtisch.date, today.value)) {
    let nextMonth = addMonths(stammtisch.date, 1);
    let start = startOfMonth(nextMonth);
    let friday = nextFriday(start);
    friday.setHours(stammtisch.date.getHours());
    friday.setMinutes(stammtisch.date.getMinutes());
    stammtisch.date = friday;
    stammtisch.edition += 1;
  }
  let jam = {
    edition: 105,
    date: new Date(2022, 9, 7, 12, 0),
    type: formats[1],
  };
  while (isBefore(jam.date, today.value)) {
    let nextMonth = addMonths(jam.date, 1);
    let start = startOfMonth(nextMonth);
    let saturday = nextSaturday(nextSaturday(nextSaturday(start)));
    saturday.setHours(jam.date.getHours());
    jam.date = saturday;
    jam.edition += 1;
  }
  let event = isBefore(jam.date, stammtisch.date) ? jam : stammtisch;
  when.value = event.date;
  format.value = event.type;
  edition.value = event.edition;
}
onMounted(generateNextEvent);
watch(today, generateNextEvent);

function download() {
  function downloadVersion(el, name, zoom) {
    el.style = `zoom: ${zoom}`;
    domtoimage
      .toPng(el, {
        width: el.clientWidth * zoom,
        height: el.clientHeight * zoom,
      })
      .then(function (blob) {
        var link = document.createElement("a");
        link.download = `${format.value}-${
          edition.value
        }-${name}-${new Date().getHours()}-${new Date().getMinutes()}.png`;
        link.href = blob;
        link.click();
        el.style = "";
      });
  }
  downloadVersion(meetup.value, "meetup", 2);
  downloadVersion(insta.value, "insta", 4);
  downloadVersion(square.value, "square", 4);
}
</script>

<style>
:root {
  font-family: "Comfortaa", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;

  --fg-1: #cb5955;
  --fg-2: #a33c3b;
}
label {
  display: block;
}
</style>

<style scoped>
form {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;

  gap: 24px;
  background: var(--fg-1);
  padding: 24px;
}
.preview {
  display: flex;
  gap: 100px;
  flex-wrap: wrap;
}
.preview > div {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.125);
}
.image-preview {
  width: 150px;
}
.main {
  width: 1200px;
  height: 676px;
}
.story {
  width: 540px;
  height: 960px;
}
.story :deep(.banner) {
  top: auto;
  bottom: 160px;
}
.square {
  width: 540px;
  height: 540px;
}
.invert :deep(.author),
.invert :deep(.site) {
  color: black;
}
.grey :deep(.author),
.grey :deep(.site) {
  color: grey;
}
.color :deep(.author),
.color :deep(.site) {
  color: var(--fg-1);
}
.bg :deep(.author),
.bg :deep(.site) {
  background: white;
  padding: 5px 10px;
}
.contain :deep(.image) {
  object-fit: contain;
}
.margin .story :deep(.image) {
  top: 100px;
  height: calc(100% - 200px);
  object-fit: cover;
}
</style>
<style src="@vueform/multiselect/themes/default.css"></style>
