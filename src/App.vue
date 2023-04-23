<template>
  <div
    id="app"
    @mouseenter.once="
      getStudentsMethod();
      setData();
    "
    @mousemove.once="setData()"
    @mousedown.once="setData()"
    @mouseleave.once="
      getStudentsMethod();
      setData();
    "
    @mouseout.once="
      getStudentsMethod();
      setData();
    "
    @mouseover.once="
      getStudentsMethod();
      setData();
    "
    @mouseup.once="setData()"
    @mousewheel.once="
      getStudentsMethod();
      setData();
    "
    @click.once="
      getStudentsMethod();
      setData();
    "
    @keydown.enter="setData"
  >
    <SearchAutocomplete :items="students" />
    <FreeClasses />
  </div>
</template>

<script>
import SearchAutocomplete from "./components/SearchAutocomplete.vue";
import setData from "./components/ShowPeriod.vue";
import FreeClasses from "./components/FreeClasses.vue";
export default {
  name: "App",
  components: {
    SearchAutocomplete,
    FreeClasses,
  },
  data() {
    return {
      students: {
        type: Object,
      },
    };
  },
  methods: {
    getStudentsMethod() {
      var students =
        "https://sostimetable-vitalik-hakim.koyeb.app/load/students";
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
