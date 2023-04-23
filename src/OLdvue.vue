<template>
  <div
    id="app"
    @mouseenter="
      getStudentsMethod();
      setData();
    "
    @mousemove="setData()"
    @mousedown="setData()"
    @mouseleave="
      getStudentsMethod();
      setData();
    "
    @mouseout="
      getStudentsMethod();
      setData();
    "
    @mouseover="
      getStudentsMethod();
      setData();
    "
    @mouseup="setData()"
    @mousewheel="
      getStudentsMethod();
      setData();
    "
    @click="
      getStudentsMethod();
      setData();
    "
    @keydown.enter="setData"
  >
    <SearchAutocomplete :items="students" />
    <!-- :items="" -->
  </div>
</template>

<script>
import SearchAutocomplete from "./components/SearchAutocomplete.vue";
// import Vue from "vue";
// import Vue3TouchEvents from "vue3-touch-events";
import setData from "./components/ShowPeriod.vue";
// import students_data from "./components/SearchAutocomplete.vue";
// Vue.use(Vue3TouchEvents);
export default {
  name: "App",
  components: {
    SearchAutocomplete,
    // ShowPeriod,
  },
  data() {
    return {
      students: {
        type: Array,
      },
    };
  },
  methods: {
    getStudentsMethod() {
      var students =
        "https:/sostimetable-vitalik-hakim.koyeb.app/load/students";
      fetch(students)
        .then((response) => {
          return response.json();
        })
        .then((myJson) => {
          // // console.log(myJson);
          // let students_data = myJson;
          // this.students_data = students_data;
          // console.log(myJson);
          // localStorage.removeItem("students");

          // localStorage.setItem("students", JSON.stringify(students_data));

          // var retrievedStudents = localStorage.getItem("students");
          // var students_array = retrievedStudents;
          this.students = myJson;
          // console.log(students_array);
          // return myJson;
        });
    },
    hello() {
      alert("Hello World");
    },
  },
  mounted() {
    // if (document.getElementById("my-datatable")) return; // was already loaded
    var scriptTag = document.createElement("script");
    scriptTag.src =
      "https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.x.x/dist/alpine.min.js";
    scriptTag.id = "";
    document.getElementsByTagName("head")[0].appendChild(scriptTag);
    var scriptTag2 = document.createElement("script");
    scriptTag.src =
      "https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js";
    scriptTag.id = "";
    document.getElementsByTagName("head")[0].appendChild(scriptTag2);
  },
  computed: {
    getStudentsComputed() {
      var retrievedStudents = localStorage.getItem("students");
      var students_array = retrievedStudents;
      // console.log(students_array);
      setData();
      return students_array;
    },
  },
};
</script>
