<template>
  <div class="cover">
    <html>
      <div>
        <center>
          <!-- <header>
    </header> -->
          <div class="logo">
            <img
              class="img-google"
              alt="Google"
              src="../assets/timetable-logo-new.png"
            />
          </div>
          <div class="bar">
            <input
              class="searchbar"
              type="text"
              title="Search"
              id="keyword"
              placeholder="Search Your Name..."
              @input="onChange"
              v-model="search"
              @keydown.down="onArrowDown"
              @keydown.up="onArrowUp"
              @keydown.enter="onEnter"
              @mouseenter.once="getStudents"
            />
          </div>
          <span id="spin"></span>
          <!-- <div class="buttons-search">
            <button class="button-search" type="button" @click="onEnter">
              Search Me!
            </button>
          </div> -->
          <div class="buttons">
            <!-- <button class="button" type="button">Free Classes</button> -->
            <a href="https://mysostimetable.web.app/">
              <button
                class="button"
                type="button"
                href="https://mysostimetable.web.app/"
              >
                Refresh & Search-Again
              </button>
            </a>
          </div>
        </center>
      </div>
    </html>
    <ul id="autocomplete-results" v-show="isOpen" class="autocomplete-results">
      <li class="loading" v-if="isLoading">Loading results...</li>
      <li
        v-else
        v-for="(result, i) in results"
        :key="i"
        @click="setResult(result)"
        class="autocomplete-result"
        :class="{ 'is-active': i === arrowCounter }"
      >
        {{ result }}
      </li>
    </ul>
    <div
      class="period"
      v-if="Object.getOwnPropertyNames(this.Period).length != 0"
    >
      <ShowPeriod />
    </div>
  </div>
</template>

<script>
// import $ from "jquery";
import ShowPeriod from "./ShowPeriod.vue";
export default {
  name: "SearchAutocomplete",
  components: {
    ShowPeriod,
  },
  props: {
    items: {
      type: Array,
      required: false,
      default: () => [],
    },
    isAsync: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  data() {
    return {
      isOpen: false,
      results: [],
      search: "",
      students_data: "",
      isLoading: false,
      arrowCounter: -1,
      url_base: "https://sos-time-table-app-backend.herokuapp.com/search/",
      query: "",
      Period: {},
      student_name: "",
      day: "1",
      this_period: "",
      this_time: "Loading",
    };
  },
  watch: {
    items: function (value, oldValue) {
      if (value.length !== oldValue.length) {
        this.results = value;
        this.isLoading = false;
      }
    },
  },
  mounted() {
    document.addEventListener("click", this.handleClickOutside);
  },
  unmounted() {
    document.removeEventListener("click", this.handleClickOutside);
  },
  methods: {
    getStudents() {
      var students =
        "https://sos-time-table-app-backend.herokuapp.com/load/students";
      fetch(students)
        .then((response) => {
          return response.json();
        })
        .then((myJson) => {
          // console.log(myJson);
          let students_data = myJson;
          this.students_data = students_data;

          localStorage.removeItem("students");

          localStorage.setItem("students", JSON.stringify(students_data));

          var retrievedStudents = localStorage.getItem("students");
          var students_array = retrievedStudents;
          this.students = students_array;
          // console.log(students_array);
          let studentsArray = JSON.stringify(students_array);
          return studentsArray;
        });
    },
    setResult(result) {
      this.search = result;
      this.isOpen = false;
      // this.student_name = document.getElementById("keyword").value;
      console.log(document.getElementById("keyword").value);
      // I will put my function to fetch here
      this.onEnterdelay();
      fetch(`https://sos-time-table-app-backend.herokuapp.com/app/failsafe`)
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    filterResults() {
      this.results = this.items.filter((item) => {
        return item.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
      });
    },
    onChange() {
      this.$emit("input", this.search);

      if (this.isAsync) {
        this.isLoading = true;
      } else {
        this.filterResults();
        this.isOpen = true;
      }
    },
    handleClickOutside(event) {
      if (!this.$el.contains(event.target)) {
        this.isOpen = false;
        this.arrowCounter = -1;
        // this.student_name = document.getElementById("keyword").value;
        // console.log(document.getElementById("keyword").value);
        // I will put my function to fetch here
        //   fetch(`${this.url_base}${this.student_name}`)
        //     .then((res) => {
        //       return res.json();
        //     })
        //     .then(this.setResults);
        //
      }
    },
    onArrowDown() {
      if (this.arrowCounter < this.results.length) {
        this.arrowCounter = this.arrowCounter + 1;
      }
    },
    onArrowUp() {
      if (this.arrowCounter > 0) {
        this.arrowCounter = this.arrowCounter - 1;
      }
    },
    onEnter() {
      this.search = this.results[this.arrowCounter];
      this.isOpen = false;
      this.arrowCounter = -1;
      this.student_name = document.getElementById("keyword").value;
      console.log(document.getElementById("keyword").value);
      var keyword = document.getElementById("keyword").value;
      if (keyword == "") {
        alert("Please enter a query");
      } else {
        // I will put my function to fetch here
        fetch(`${this.url_base}${this.student_name}`)
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }

      localStorage.setItem("SEARCHED", "1");
    },
    onEnterdelay() {
      function sleep(time) {
        return new Promise((resolve) => setTimeout(resolve, time));
      }
      // this.setResult("Searching..")
      // Usage!
      sleep(5).then(() => {
        // Do something after the sleep!
        this.search = this.results[this.arrowCounter];
        this.isOpen = false;
        this.arrowCounter = -1;
        this.student_name = document.getElementById("keyword").value;
        console.log(document.getElementById("keyword").value);
        var keyword = document.getElementById("keyword").value;
        if (keyword == "") {
          alert("Please enter a query");
        } else {
          // I will put my function to fetch here
          fetch(`${this.url_base}${this.student_name}`)
            .then((res) => {
              return res.json();
            })
            .then(this.setResults);
        }

        localStorage.setItem("SEARCHED", "1");
      });
    },
    setResults(results) {
      if (results === "No subject here") {
        alert(results);
      } else if (results === "Error: Beyond School day Hours") {
        alert(results);
      } else if (results === "Couldn't find your name in the database!") {
        alert(results);
      } else {
        this.Period = results[0];
        var period_one = results[0];
        var period_two = results[1];
        var period_three = results[2];
        var period_four = results[3];

        console.log(this.Period);
        // console.log(results[1])
        let time_raw = results[4];
        console.log("Time:" + time_raw);
        String.prototype.toHHMMSS = function () {
          var sec_num = parseInt(this, 10); // don't forget the second param
          var hours = Math.floor(sec_num / 3600);
          var minutes = Math.floor((sec_num - hours * 3600) / 60);
          var seconds = sec_num - hours * 3600 - minutes * 60;

          if (hours < 10) {
            hours = "0" + hours;
          }
          if (minutes < 10) {
            minutes = "0" + minutes;
          }
          if (seconds < 10) {
            seconds = "0" + seconds;
          }
          return hours + ":" + minutes;
        };

        var time = `${time_raw}`.toHHMMSS();
        console.log(`${time_raw}`.toHHMMSS());
        // Store time  future use
        localStorage.removeItem("time");

        localStorage.setItem("time", time);

        var retrievedTime = localStorage.getItem("time");
        this.this_time = retrievedTime;
        // Store periods
        // Period One
        localStorage.removeItem("PeriodOne");
        localStorage.setItem("PeriodOne", JSON.stringify(period_one));
        var retrievedObjectOne = localStorage.getItem("PeriodOne");
        console.log("retrievedObject: ", JSON.parse(retrievedObjectOne));
        var parsedObjectOne = JSON.parse(retrievedObjectOne);
        console.log(parsedObjectOne["1"]);
        // localStorage.setItem("Subject", this.Period);
        // const Subject = localStorage.getItem("Subject");
        // console.log(Subject);

        //Period Two
        localStorage.removeItem("PeriodTwo");
        localStorage.setItem("PeriodTwo", JSON.stringify(period_two));
        var retrievedObjectTwo = localStorage.getItem("PeriodTwo");
        console.log("retrievedObject: ", JSON.parse(retrievedObjectTwo));
        var parsedObjectTwo = JSON.parse(retrievedObjectTwo);
        console.log(parsedObjectTwo["1"]); // This is the day = 1

        // Period Three
        localStorage.removeItem("PeriodThree");
        localStorage.setItem("PeriodThree", JSON.stringify(period_three));
        var retrievedObjectThree = localStorage.getItem("PeriodTwo");
        console.log("retrievedObject: ", JSON.parse(retrievedObjectThree));
        var parsedObjectThree = JSON.parse(retrievedObjectThree);
        console.log(parsedObjectThree["1"]); // This is the day = 1

        // Period Four
        // Period Three
        localStorage.removeItem("PeriodFour");
        localStorage.setItem("PeriodFour", JSON.stringify(period_four));
        var retrievedObjectFour = localStorage.getItem("PeriodFour");
        console.log("retrievedObject: ", JSON.parse(retrievedObjectFour));
        var parsedObjectFour = JSON.parse(retrievedObjectFour);
        console.log(parsedObjectFour["1"]); // This is the day = 1
        localStorage.removeItem("SEARCHED");

        localStorage.setItem("SEARCHED", "1");
      }
    },
  },
};
</script>

<style>
html,
body {
  position: relative;
  height: 100%;
  margin: 0;
  padding: 0;
}
body {
  background-color: #eeeeee;
  font-family: "Open Sans", "Helvetica Neue", sans-serif;
  font-size: 16px;
  transform: translate3d(0, 0, 0);
  background: #1fa2ff; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #1fa2ff,
    #12d8fa,
    #a6ffcb
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #1fa2ff,
    #12d8fa,
    #a6ffcb
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr="#1e5799", endColorstr="#7db9e8",GradientType=1 );
}
/* .search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
} */
.autocomplete-results {
  position: relative;
  padding: 0;
  margin: 0;
  border: 1px solid #eeeeee;
  height: 150px;
  width: 500px;
  margin-left: 400px;
  border-radius: 5px;
  overflow: auto;
  font-family: "Open Sans", "Helvetica Neue", sans-serif;
  /* font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif; */
}

.autocomplete-result {
  list-style: none;
  border: #000;
  text-align: left;
  padding: 2px 2px;
  cursor: pointer;
  color: #000000;
  background: #eeeeee;
}

.autocomplete-result.is-active,
.autocomplete-result:hover {
  background-color: crimson;
  color: white;
}
/*--------------------
container
--------------------*/
/* .wrap {
  margin: 150px auto 30px;
  position: relative;
  width: 460px;
  background: #fff;
  border-radius: 15px;
  padding: 272px 45px 30px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
} */

/* /*--------------------
confirmation
--------------------*/
/* .confirmation {
  position: absolute;
  top: 96px;
  left: 0;
  right: 0;
  opacity: 0;
  transition: opacity 300ms ease 300ms;
}
.confirmation.visible {
  opacity: 1;
}

.all-good {
  display: block;
  margin: 40px auto 0;
  width: 60px;
}

.apple-logo {
  fill: #fff;
  display: block;
  margin: 0 auto;
  width: 80px;
}

.path {
  stroke-dasharray: 1000;
  stroke-dashoffset: 0;
}
.path.circle {
  -webkit-animation: dash 0.9s ease-in-out;
  animation: dash 0.9s ease-in-out;
}
.path.line {
  stroke-dashoffset: 1000;
  -webkit-animation: dash 0.9s 0.35s ease-in-out forwards;
  animation: dash 0.9s 0.35s ease-in-out forwards;
}
.path.check {
  stroke-dashoffset: -100;
  -webkit-animation: dash-check 0.9s 0.35s ease-in-out forwards;
  animation: dash-check 0.9s 0.35s ease-in-out forwards;
}

p {
  text-align: center;
  margin: 20px 0 60px;
  font-size: 1.25em;
}
p.success {
  color: #777;
}

@-webkit-keyframes dash {
  0% {
    stroke-dashoffset: 1000;
  }
  100% {
    stroke-dashoffset: 0;
  }
}
@keyframes dash {
  0% {
    stroke-dashoffset: 1000;
  }
  100% {
    stroke-dashoffset: 0;
  }
}
@-webkit-keyframes dash-check {
  0% {
    stroke-dashoffset: -100;
  }
  100% {
    stroke-dashoffset: 900;
  }
}
@keyframes dash-check {
  0% {
    stroke-dashoffset: -100;
  }
  100% {
    stroke-dashoffset: 900;
  }
}
/*--------------------
Buttons
--------------------*/
/* .button-cnt {
  display: flex;
  justify-content: space-around;
  width: 100%;
}


/* SEARCH BUTTON */
/* ul {
  list-style-type: none;
  overflow: hidden;
}

li {
  float: right;
}

li a {
  color: #000;
  display: block;
  text-align: center;
  padding: 10px 10px;
  text-decoration: none;
  font-size: 14px;
}
li a:hover {
  text-decoration: underline;
} */
/* .grid {
  height: 23px;
  position: relative;
  bottom: 4px;
}
.signbutton {
  background-color: #4885ed;
  color: #fff;
  border: none;
  border-radius: 3px;
  padding: 7px 10px;
  position: relative;
  bottom: 7px;
  font-weight: bold;
} */
.logo {
  margin-top: 50px;
  margin-bottom: 20px;
}
.bar {
  margin: 0 auto;
  width: 575px;
  border-radius: 30px;
  border: 1px solid #dcdcdc;
  background: white;
}
.bar:hover {
  box-shadow: 1px 1px 8px 1px #dcdcdc;
}
.bar:focus-within {
  box-shadow: 1px 1px 8px 1px #dcdcdc;
  outline: none;
}
.searchbar {
  height: 50px;
  border: none;
  width: 500px;
  border-radius: 30px;
  font-size: 18px;
  font-family: "Open Sans", "Helvetica Neue", sans-serif;
  margin: 0 auto;
  outline: none;
}
.voice {
  height: 20px;
  position: relative;
  top: 0px;
  left: 25%;
}
.buttons {
  margin-top: 10px;
}
.buttons-search {
  margin-top: 10px;
}
.button {
  background-color: #ff0000;
  border: none;
  color: #ffffff;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button:hover {
  border: 1px solid #c8c8c8;
  padding: 9px 19px;
  color: #fff9f9;
}
.button:focus {
  border: 1px solid #4885ed;
  padding: 9px 19px;
}

.button-search {
  background-color: crimson;
  border: none;
  color: #ffffff;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button-search:hover {
  border: 1px solid #c8c8c8;
  padding: 9px 19px;
  color: #fdfdfd;
}
.button-search:focus {
  border: 1px solid #4885ed;
  padding: 9px 19px;
}
.img-google {
  border-radius: 50%;
}
/* .search {
  position: relative;
  top: 0%;
} */
#spin {
  color: rgb(0, 0, 0);
  font-size: 18px;
  font-family: "Open Sans", "Helvetica Neue", sans-serif;
}
#spin:after {
  content: "";
  animation: spin 80s linear infinite;
}
@keyframes spin {
  0% {
    content: "Refresh the page before searching another name";
  }
  10% {
    content: "Refresh the page before searching another name";
  }
  20% {
    content: "Move your mouse over the page rapidly to get the results faster";
  }
  30% {
    content: "Move your mouse over the page rapidly to get the results faster";
  }
  40% {
    content: "Always choose your name  from the suggestions to prevent errors";
  }
  50% {
    content: "Always choose your name  from the suggestions to prevent errors";
  }
  60% {
    content: "Refresh or move mouse rapidly to load suggestions";
  }
  70% {
    content: "Refresh or move mouse rapidly to load suggestions";
  }
  80% {
    content: "Refresh the page before searching another";
  }
  90% {
    content: "Refresh the page before searching another";
  }
  100% {
    content: "Report issue when there is a mistake or error code eg. 404";
  }
}
</style>
