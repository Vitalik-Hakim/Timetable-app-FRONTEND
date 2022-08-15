<template>
  <div class="cover">
    <html>
      <div>
        <center>
          <!-- <header>
    </header> -->
          <div class="logo">
            <img
              alt="Google"
              src="data:image/png;base64,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"
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
              @mouseenter="getStudents"
            />
          </div>
          <span id="spin"></span>
          <div class="buttons-search">
            <button class="button-search" type="button" @click="onEnter">
              Search Me!
            </button>
          </div>
          <div class="buttons">
            <button class="button" type="button">Free Classes</button>
            <button class="button" type="button">Report Issue</button>
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
      url_base: "http://127.0.0.1:8000/search/",
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
      var students = "http://127.0.0.1:8000/load/students";
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
      fetch(`http://127.0.0.1:8000/app/failsafe`)
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
      localStorage.removeItem("SEARCHED");

      localStorage.setItem("SEARCH", "1");
    },
    onEnterdelay() {
      function sleep(time) {
        return new Promise((resolve) => setTimeout(resolve, time));
      }
      // this.setResult("Searching..")
      // Usage!
      sleep(5000).then(() => {
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
        localStorage.removeItem("SEARCHED");

        localStorage.setItem("SEARCH", "1");
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
  font-family: "helvetica", sans-serif;
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
  font-family: "Courier New", Courier, monospace;
}

.autocomplete-result {
  list-style: none;
  border: #000;
  text-align: left;
  padding: 2px 2px;
  cursor: pointer;
  color: #0dcf95;
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
  font-family: "Courier New", Courier, monospace;
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
  background-color: #f5f5f5;
  border: none;
  color: #707070;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button:hover {
  border: 1px solid #c8c8c8;
  padding: 9px 19px;
  color: #808080;
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
img {
  border-radius: 50%;
}
/* .search {
  position: relative;
  top: 0%;
} */
#spin {
  color: rgb(0, 0, 0);
  font-size: 18px;
  font-family: "Courier New", Courier, monospace;
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
