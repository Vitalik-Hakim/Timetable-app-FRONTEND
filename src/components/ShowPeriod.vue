<template>
  <!-- partial:index.partial.html -->
  <div
    class="container"
    @mouseenter="setData"
    @mousemove.once="setData"
    @mousedown.once="setData"
    @mouseleave.once="setData"
    @mouseout.once="setData"
    @mouseover.once="setData"
    @mouseup.once="setData"
    @mousewheel.once="setData"
    @keydown.enter="setData"
  >
    <!-- Loading Div -->
    <div id="myModal" class="modal-loading" v-if="this_loading_div">
      <!-- Modal content -->
      <div class="modal-content-loading">
        <span class="close">&times;</span>
        <div
          class="element-card-loading"
          @click="jqed"
          @mouseenter="removeLoading"
          v-if="this_loading_div"
        >
          <div class="front-facing">
            <h1 class="abr">LOADING</h1>
            <p class="title">Timetable</p>
            <span class="atomic-number"
              ><div class="status-circle-loading">
                <div class="status-circle-yellow-loading"></div>
                <div class="status-circle-red-loading"></div></div
            ></span>
            <span class="atomic-mass">Please Wait</span>
          </div>
          <button class="flip-btn" @click="jqed">Flip Card</button>
          <!-- Duplicating if its element split -->
        </div>
        <p>Some text in the Modal..</p>
      </div>
    </div>

    <button
      v-if="iS_Loaded"
      @click="hidebtn"
      class="button-timetable"
      @mouseover.once="hidebtn"
      @mousemove.once="hidebtn"
    >
      Click to Get Timetable
    </button>
    <!-- Loading Div -->
    <div class="element-card" @click="jqed" v-if="isNotSplit_one">
      <!-- First Card -->
      <!-- isNotSplit -->
      <div class="front-facing" @click="jqed">
        <h1 class="abr" @click="jqed">
          <div class="status-circle"></div>
          {{ this_period_one }}
        </h1>
        <p class="title" @click="jqed">{{ this_current_period_one }}</p>
        <span class="atomic-number" @click="jqed">{{ this_room_one }}</span>
        <span class="atomic-mass" @click="jqed">{{ this_teacher_one }}</span>
        <span class="atomic-mass-1" @click="jqed">
          <h4>{{ this_ends }}</h4>
          {{ this_time }}</span
        >
        <button class="flip-btn" @click="jqed">Flip Card</button>
        <!-- Duplicating if its element split -->
      </div>

      <div class="back-facing">
        <h4>Subject:</h4>
        <b>{{ this_teacher_one }} </b> <br />
        <h4>ClassRoom:</h4>
        <b> {{ this.teachers[this_period_one] }} </b> <br />
        <h4>Teacher:</h4>
        <b>{{ this.teachers[this_room_one] }} </b> <br />
        <p>
          <button class="flip-btn" @click="jqed_reverse">Flip Back</button>
        </p>
      </div>
    </div>
    <!-- Element-split One-->
    <div class="element-card-split-container" v-if="isSplit_one">
      <div class="status-circle" v-if="isSplit_one"></div>
      <div class="element-card-split-1-final" @click="jqed">
        <div class="front-facing" @click="jqed">
          <span class="abr" @click="jqed">
            <div class="status-circle" v-if="isSplit_one"></div>
            {{ this_period_split_one1 }}
          </span>
          <p class="title" @click="jqed">{{ this_current_period }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_one1
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_one1
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_one1 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_one1 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_one1 }} </b> <br />
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
      <div class="element-card-split-2-final" @click="jqed" v-if="isSplit_one">
        <div class="front-facing" @click="jqed">
          <span class="abr" @click="jqed">
            {{ this_period_split_one2 }}
            <div class="status-circle"></div>
          </span>
          <p class="title" @click="jqed">{{ this_current_period }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_one2
          }}</span>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_one2
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_one2
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_one2 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_one2 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_one2 }} </b> <br />
          <!-- <p>
            <button class="flip-btn" @click="jqed_reverse">Flip Back</button>
          </p> -->
        </div>
      </div>
    </div>

    <!-- Second Card -->
    <div class="element-card" @click="jqed" v-if="isNotSplit_two">
      <div class="front-facing" @click="jqed">
        <h1 class="abr" @click="jqed">
          {{ this_period_two }}
          <div class="status-circle-red"></div>
        </h1>
        <p class="title" @click="jqed">{{ this_current_period_two }}</p>
        <span class="atomic-number" @click="jqed">{{ this_room_two }}</span>
        <span class="atomic-number-1" @click="jqed">
          <!-- <h4>{{ this_starts }}</h4>
          {{ this_time2 }} -->
        </span>
        <span class="atomic-mass" @click="jqed">{{ this_teacher_two }}</span>
        <button class="flip-btn" @click="jqed">Flip Card</button>
      </div>
      <div class="back-facing">
        <h4>Subject:</h4>
        <b>{{ this_teacher_two }} </b> <br />
        <h4>ClassRoom:</h4>
        <b> {{ this.teachers[this_period_two] }} </b> <br />
        <h4>Teacher:</h4>
        <b>{{ this.teachers[this_room_two] }} </b> <br />
        <p>
          <button class="flip-btn" @click="jqed_reverse">Flip Back</button>
        </p>
      </div>
    </div>
    <!-- Element-Split Two-->
    <div class="element-card-split-container" v-if="isSplit_two">
      <div class="status-circle-red" v-if="isSplit_two"></div>
      <div class="element-card-split-1-final" @click="jqed">
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            <!-- <div class="status-circle-red" v-if="isSplit_two"></div> -->
            {{ this_period_split_two1 }}
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_two1 }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_two1
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_two1
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_two1 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_two1 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_two1 }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
      <div class="element-card-split-2-final" @click="jqed" v-if="isSplit_two">
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            {{ this_period_split_two2 }}
            <!-- <div class="status-circle"></div> -->
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_two2 }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_two2
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_two2
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_two2 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_two2 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_two2 }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
    </div>

    <!-- Third Card -->
    <div class="element-card" @click="jqed" v-if="isNotSplit_three">
      <div class="front-facing" @click="jqed">
        <h1 class="abr" @click="jqed">
          {{ this_period_three }}
          <div class="status-circle-red"></div>
        </h1>
        <p class="title" @click="jqed">{{ this_current_period_three }}</p>
        <span class="atomic-number" @click="jqed">{{ this_room_three }}</span>
        <span class="atomic-number-1" @click="jqed">
          <!-- <h4>{{ this_starts }}</h4>
          {{ this_time2 }} -->
        </span>
        <span class="atomic-mass" @click="jqed">{{ this_teacher_three }}</span>
        <button class="flip-btn" @click="jqed">Flip Card</button>
      </div>
      <div class="back-facing">
        <h4>Subject:</h4>
        <b>{{ this_teacher_three }} </b> <br />
        <h4>ClassRoom:</h4>
        <b> {{ this.teachers[this_period_three] }} </b> <br />
        <h4>Teacher:</h4>
        <b>{{ this.teachers[this_room_three] }} </b> <br />
        <p>
          <button class="flip-btn" @click="jqed_reverse">Flip Back</button>
        </p>
      </div>
    </div>
    <div class="element-card-split-container" v-if="isSplit_three">
      <!-- Element-Split Three -->
      <div class="status-circle-red" v-if="isSplit_three"></div>
      <div class="element-card-split-1-final" @click="jqed">
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            <!-- <div class="status-circle-red" v-if="isSplit_three"></div> -->
            {{ this_period_split_three1 }}
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_three }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_three1
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_three1
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_three1 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_three1 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_three1 }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
      <div
        class="element-card-split-2-final"
        @click="jqed"
        v-if="isSplit_three"
      >
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            {{ this_period_split_three2 }}
            <!-- <div class="status-circle"></div> -->
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_three }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_three2
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_three2
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_three2 }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_three2 }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_three2 }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
    </div>

    <!-- Fourth Card -->
    <div class="element-card" @click="jqed" v-if="isNotSplit_four">
      <div class="front-facing" @click="jqed">
        <h1 class="abr" @click="jqed">
          {{ this_period_four }}
          <div class="status-circle-red"></div>
        </h1>
        <p class="title" @click="jqed">{{ this_current_period_four }}</p>
        <span class="atomic-number" @click="jqed">{{ this_room_four }}</span>
        <span class="atomic-number-1" @click="jqed">
          <!-- <h4>{{ this_starts }}</h4>
          {{ this_time3 }} -->
        </span>
        <span class="atomic-mass" @click="jqed">{{ this_teacher_four }}</span>
        <button class="flip-btn" @click="jqed">Flip Card</button>
      </div>
      <div class="back-facing">
        <h4>Subject:</h4>
        <b>{{ this_teacher_four }} </b> <br />
        <h4>ClassRoom:</h4>
        <b> {{ this.teachers[this_period_four] }} </b> <br />
        <h4>Teacher:</h4>
        <b>{{ this.teachers[this_room_four] }} </b> <br />
        <p>
          <button class="flip-btn" @click="jqed_reverse">Flip Back</button>
        </p>
      </div>
    </div>
    <!-- Element-split Four -->
    <div class="element-card-split-container" v-if="isSplit_four">
      <div class="status-circle-red" v-if="isSplit_four"></div>
      <div class="element-card-split-1-final" @click="jqed">
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            <!-- <div class="status-circle-red" v-if="isSplit_four"></div> -->
            {{ this_period_split_four }}
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_four }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_four
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_four
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_four }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_four }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_four }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
      <div class="element-card-split-2-final" @click="jqed" v-if="isSplit_four">
        <div class="front-facing" @click="jqed">
          <h1 class="abr" @click="jqed">
            {{ this_period_four }}
            <!-- <div class="status-circle"></div> -->
          </h1>
          <p class="title" @click="jqed">{{ this_current_period_three }}</p>
          <span class="atomic-number" @click="jqed">{{
            this_room_split_four
          }}</span>
          <span class="atomic-mass" @click="jqed">{{
            this_teacher_split_four
          }}</span>
          <!-- <button class="flip-btn" @click="jqed">Flip Card</button> -->
        </div>
        <div class="back-facing">
          <!-- <h4>Subject:</h4> -->
          <b>{{ this_teacher_split_four }} </b> <br />
          <!-- <h4>ClassRoom:</h4> -->
          <b> {{ this_period_split_four }} </b> <br />
          <!-- <h4>Teacher:</h4> -->
          <b>{{ this_room_split_four }} </b> <br />
          <p></p>
          <p>
            <!-- <button class="flip-btn" @click="jqed_reverse">Flip Back</button> -->
          </p>
        </div>
      </div>
    </div>
  </div>

  <button
    class="button-2"
    href="https://forms.gle/4nwVW75dKLGu6btZ8"
    target="_blank"
  >
    <a href="https://forms.gle/4nwVW75dKLGu6btZ8" target="_blank"
      >Report Issues</a
    >
  </button>
  <button
    class="button-3"
    href="https://forms.gle/4nwVW75dKLGu6btZ8"
    target="_blank"
  >
    <a href="https://github.com/Vitalik-Hakim" target="_blank">Made with ❤️</a>
  </button>
</template>

<script>
import jquery from "jquery";
export default {
  name: "ShowPeriod",
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
      this_period_one: "Loading Data",
      this_teacher_one: "Loading Data",
      this_room_one: "Loading Data",
      this_teacher_split_one: "Loading Data",
      this_period_split_one: "Loading Data",
      this_room_split_one: "Loading Data",
      this_time: "Loading Data",
      this_time1: "Loading Data",
      this_time2: "Loading Data",
      this_time3: "Loading Data",
      this_time4: "Loading Data",
      this_link: "Loading Data",
      this_ends: "Started:",
      this_starts: "Starts:",
      isSearch: false,
      iS_Loaded: true,
      result_bool: false,
      teachers: {
        type: Object,
      },
      this_current_period_one: "Current Period",
      this_period_two: "Loading Data",
      this_teacher_two: "Loading Data",
      this_room_two: "Loading Data",
      this_teacher_split_two: "Loading Data",
      this_period_split_two: "Loading Data",
      this_room_split_two: "Loading Data",
      this_current_period_two: "Next Period",
      this_period_three: "Loading Data",
      this_teacher_three: "Loading Data",
      this_room_three: "Loading Data",
      this_teacher_split_three: "Loading Data",
      this_period_split_three: "Loading Data",
      this_room_split_three: "Loading Data",
      this_current_period_three: "Next Period(Three)",
      this_period_four: "Loading Data",
      this_teacher_four: "Loading Data",
      this_room_four: "Loading Data",
      this_teacher_split_four: "Loading Data",
      this_period_split_four: "Loading Data",
      this_room_split_four: "Loading Data",
      this_current_period_four: "Next Period(FOUR)",
      this_period_split_one1: "Loading Data",
      this_room_split_one1: "Loading Data",
      this_teacher_split_one1: "Loading Data",
      this_period_split_two1: "Loading Data",
      this_room_split_two1: "Loading Data",
      this_teacher_split_two1: "Loading Data",
      this_period_split_three1: "Loading Data",
      this_room_split_three1: "Loading Data",
      this_teacher_split_three1: "Loading Data",
      this_period_split_four1: "Loading Data",
      this_room_split_four1: "Loading Data",
      this_teacher_split_four1: "Loading Data",
      this_period_split_one2: "Loading Data",
      this_room_split_one2: "Loading Data",
      this_teacher_split_one2: "Loading Data",
      this_period_split_two2: "Loading Data",
      this_room_split_two2: "Loading Data",
      this_teacher_split_two2: "Loading Data",
      this_period_split_three2: "Loading Data",
      this_room_split_three2: "Loading Data",
      this_teacher_split_three2: "Loading Data",
      this_period_split_four2: "Loading Data",
      this_room_split_four2: "Loading Data",
      this_teacher_split_four2: "Loading Data",
      isSplit: false,
      isSplit_one: false,
      isSplit_two: false,
      isSplit_three: false,
      isNoSplit_four: false,
      isNotSplit_one: false,
      isNotSplit_two: false,
      isNotSplit_three: false,
      isNotSplit_four: false,
      isNotSplit: false,
      url_base: "https://sostimetable-vitalik-hakim.koyeb.app/search/",
      query: "",
      Period: {},
      this_loading_div: true,
    };
  },

  methods: {
    removeLoading() {
      this.this_loading_div = false;
    },
    loadingmodal() {
      // Get the modal
      var modal = document.getElementById("myModal");

      // Get the button that opens the modal
      var btn = document.getElementById("myBtn");

      // Get the <span> element that closes the modal
      var span = document.getElementsByClassName("close")[0];

      // When the user clicks the button, open the modal
      btn.onclick = function () {
        modal.style.display = "block";
      };

      // When the user clicks on <span> (x), close the modal
      span.onclick = function () {
        modal.style.display = "none";
      };

      // When the user clicks anywhere outside of the modal, close it
      window.onclick = function (event) {
        if (event.target == modal) {
          modal.style.display = "none";
        }
      };
    },
    setData() {
      const dayIndex = new Date().getDay();
      const getDayName = (dayIndex) => {
        const days = [
          "Sunday",
          "Monday",
          "Tuesday",
          "Wednesday",
          "Thursday",
          "Friday",
          "Saturday",
        ];
        return days[dayIndex];
      };
      const today = getDayName(dayIndex);
      console.log(today);
      //FETCH PERIODS ONE BY ONE (REALLY BAD BUT IT WORKS)
      //   let today = "monday";
      function getDay(day) {
        if (day === "Monday") {
          // statement
          return "1";
        } else if (day === "Tuesday") {
          // statement
          return "2";
        } else if (day === "Wednesday") {
          // statement
          return "3";
        } else if (day === "Thursday") {
          return "4";
        } else if (day === "Friday") {
          // statement
          return "5";
        } else {
          // statement
          return "0";
        }
      }
      // const today_number = "2";
      const today_number = getDay(today);
      console.log(today_number);

      // #Period One
      //   this.this_period = localStorage.getItem("Subject");
      var retrievedObjectOne = localStorage.getItem(`PeriodOne`);
      console.log("retrievedObject: ", JSON.parse(retrievedObjectOne));
      var parsedObjectOne = JSON.parse(retrievedObjectOne);
      var subjectold_one = parsedObjectOne;
      // Get time
      // var today_DATE = new Date();
      // var date_DATE =
      //   today_DATE.getFullYear() +
      //   "-" +
      //   (today_DATE.getMonth() + 1) +
      //   "-" +
      //   today_DATE.getDate();
      // var time =
      //   today_DATE.getHours() + ":" + today_DATE.getMinutes() + ":" + today.getSeconds();
      // var dateTime = date_DATE+ " " + time;

      // console.log(dateTime);
      // var myArray = dateTime.split(" ");

      // localStorage.setItem("time", myArray[1]);
      // var retrievedTimeOne = localStorage.getItem("time1");
      // var retrievedTimeOne = localStorage.getItem("time1");
      var retrievedTimeOne = localStorage.getItem("time1");
      var retrievedTime_dup = localStorage.getItem("time");
      var retrievedTime_two = localStorage.getItem("time2");
      var retrievedTime_three = localStorage.getItem("time3");
      var retrieved_link = localStorage.getItem("link");
      this.this_time1 = retrievedTimeOne;
      this.this_time = retrievedTime_dup;
      // if (isNaN(retrievedTimeOne)) {
      //   this.this_time = retrievedTime_dup;
      // } else {
      //   this.this_time = retrievedTimeOne;
      // }
      console.log(retrievedTime_dup);
      this.this_time2 = retrievedTime_two;
      this.this_time3 = retrievedTime_three;
      this.this_link = retrieved_link;
      //   console.log("here: " + subjectold);
      //   var subjectoldat = subjectold.replace(/(?:\r\n|\r|\n)/g, "@");
      var subjectoldatOne = subjectold_one.replace("/", "-");
      var urlOne = `https://sostimetable-vitalik-hakim.koyeb.app/process/${subjectoldatOne}`;

      //   console.log(subjectold);
      fetch(urlOne)
        .then((response_one) => {
          return response_one.json();
        })
        .then((myJson_one) => {
          //   var newParsedObject = JSON.parse(myJson);
          console.log("My" + myJson_one);
          let result_one = myJson_one.includes("&&");
          if (result_one === true) {
            let resultZero_one = myJson_one.split("&&");
            console.log(resultZero_one);
            this.isSplit_one = true;
            let resultTwo_one = resultZero_one[0];
            let resultThree_one = resultZero_one[1];
            console.log(resultTwo_one);
            console.log(resultThree_one);
            // console.log(resultTwo)
            // const resultThree = resultZero[1]
            // result two
            resultTwo_one = resultTwo_one.split(/\r?\n/);
            const filtered_resultTwo_one = resultTwo_one.filter((n) => n);
            let subject_one = filtered_resultTwo_one[1];
            let teacher_one = filtered_resultTwo_one[0];
            let room_one = filtered_resultTwo_one[2];
            this.this_teacher_split_one1 = teacher_one;
            this.this_period_split_one1 = subject_one;
            this.this_room_split_one1 = room_one;

            /// Split period
            resultThree_one = resultThree_one.split(/\r?\n/);
            const filtered_resultThree_one = resultThree_one.filter((n) => n);
            let subject_split_two = filtered_resultThree_one[1];
            let teacher_split_two = filtered_resultThree_one[0];
            let room_split_two = filtered_resultThree_one[2];
            // // result three
            // var subject = resultFour[2];
            // var teacher = resultFour[0];
            // var room = resultFour[4];
            this.this_teacher_split_one2 = teacher_split_two;
            this.this_period_split_one2 = subject_split_two;
            this.this_room_split_one2 = room_split_two;
          } else {
            this.isNotSplit_one = true;
            const resultFour_one = myJson_one.split(/\r?\n/);
            console.log(resultFour_one);
            const filtered_resultThree_one = resultFour_one.filter((n) => n);
            console.log("Final List" + filtered_resultThree_one);
            var subject_one = filtered_resultThree_one[1];
            var teacher_one = filtered_resultThree_one[0];
            var room_one = filtered_resultThree_one[2];

            //   subject = subject.replace(/(\r\n|\n|\r)/gm, "");
            this.this_teacher_one = teacher_one;
            this.this_period_one = subject_one;
            this.this_room_one = room_one;
          }
        });
      // #Period Two
      //   this.this_period = localStorage.getItem("Subject");
      var retrievedObjectTwo = localStorage.getItem(`PeriodTwo`);
      console.log("retrievedObject: ", JSON.parse(retrievedObjectTwo));
      var parsedObjectTwo = JSON.parse(retrievedObjectTwo);
      var subjectold_two = parsedObjectTwo;
      // Get time
      // var retrievedTimeTwo = localStorage.getItem("time");

      // this.this_time = retrievedTimeTwo;
      //   console.log("here: " + subjectold);
      //   var subjectoldat = subjectold.replace(/(?:\r\n|\r|\n)/g, "@");
      var subjectoldatTwo = subjectold_two.replace("/", "-");
      //   console.log(subjectold);
      var urlTwo = `https://sostimetable-vitalik-hakim.koyeb.app/process/${subjectoldatTwo}`;

      fetch(urlTwo)
        .then((response_two) => {
          return response_two.json();
        })
        .then((myJson_two) => {
          //   var newParsedObject = JSON.parse(myJson);
          console.log("My" + myJson_two);
          let result_two = myJson_two.includes("&&");
          if (result_two === true) {
            let resultZero_two = myJson_two.split("&&");
            console.log(resultZero_two);
            this.isSplit_two = true;
            let resultTwo_two = resultZero_two[0];
            let resultThree_two = resultZero_two[1];
            console.log(resultTwo_two);
            console.log(resultThree_two);
            // console.log(resultTwo)
            // const resultThree = resultZero[1]
            // result two
            resultTwo_two = resultTwo_two.split(/\r?\n/);
            const filtered_resultTwo_two = resultTwo_two.filter((n) => n);
            let subject_two = filtered_resultTwo_two[1];
            let teacher_two = filtered_resultTwo_two[0];
            let room_two = filtered_resultTwo_two[2];
            this.this_teacher_split_two1 = teacher_two;
            this.this_period_split_two1 = subject_two;
            this.this_room_split_two1 = room_two;

            /// Split period
            resultThree_two = resultThree_two.split(/\r?\n/);
            const filtered_resultThree_two = resultThree_two.filter((n) => n);
            let subject_split_two = filtered_resultThree_two[1];
            let teacher_split_two = filtered_resultThree_two[0];
            let room_split_two = filtered_resultThree_two[2];
            // // result three
            // var subject = resultFour[2];
            // var teacher = resultFour[0];
            // var room = resultFour[4];
            this.this_teacher_split_two2 = teacher_split_two;
            this.this_period_split_two2 = subject_split_two;
            this.this_room_split_two2 = room_split_two;
          } else {
            this.isNotSplit_two = true;
            const resultFour_two = myJson_two.split(/\r?\n/);
            console.log(resultFour_two);
            const filtered_resultThree_two = resultFour_two.filter((n) => n);
            console.log("Final List" + filtered_resultThree_two);
            var subject_two = filtered_resultThree_two[1];
            var teacher_two = filtered_resultThree_two[0];
            var room_two = filtered_resultThree_two[2];

            //   subject = subject.replace(/(\r\n|\n|\r)/gm, "");
            this.this_teacher_two = teacher_two;
            this.this_period_two = subject_two;
            this.this_room_two = room_two;
          }
        });

      // Period Three
      // #Period Three
      //   this.this_period = localStorage.getItem("Subject");
      var retrievedObjectThree = localStorage.getItem(`PeriodThree`);
      console.log("retrievedObject: ", JSON.parse(retrievedObjectThree));
      var parsedObjectThree = JSON.parse(retrievedObjectThree);
      var subjectold_three = parsedObjectThree;
      // Get time
      // var retrievedTimeThree = localStorage.getItem("time");

      // this.this_time = retrievedTimeThree;
      //   console.log("here: " + subjectold);
      //   var subjectoldat = subjectold.replace(/(?:\r\n|\r|\n)/g, "@");
      var subjectoldatThree = subjectold_three.replace("/", "-");
      //   console.log(subjectold);
      var urlThree = `https://sostimetable-vitalik-hakim.koyeb.app/process/${subjectoldatThree}`;
      fetch(urlThree)
        .then((response_three) => {
          return response_three.json();
        })
        .then((myJson_three) => {
          //   var newParsedObject = JSON.parse(myJson);
          console.log("My" + myJson_three);
          let result_three = myJson_three.includes("&&");
          if (result_three === true) {
            let resultZero_three = myJson_three.split("&&");
            console.log(resultZero_three);
            this.isSplit_three = true;
            let resultTwo_three = resultZero_three[0];
            let resultThree_three = resultZero_three[1];
            console.log(resultTwo_three);
            console.log(resultThree_three);
            // console.log(resultTwo)
            // const resultThree = resultZero[1]
            // result two
            resultTwo_three = resultTwo_three.split(/\r?\n/);
            const filtered_resultTwo_three = resultTwo_three.filter((n) => n);
            let subject_three = filtered_resultTwo_three[1];
            let teacher_three = filtered_resultTwo_three[0];
            let room_three = filtered_resultTwo_three[2];
            this.this_teacher_split_three1 = teacher_three;
            this.this_period_split_three1 = subject_three;
            this.this_room_split_three1 = room_three;

            /// Split period
            resultThree_three = resultThree_three.split(/\r?\n/);
            const filtered_resultThree_three = resultThree_three.filter(
              (n) => n
            );
            let subject_split_three = filtered_resultThree_three[1];
            let teacher_split_three = filtered_resultThree_three[0];
            let room_split_three = filtered_resultThree_three[2];
            // // result three
            // var subject = resultFour[2];
            // var teacher = resultFour[0];
            // var room = resultFour[4];
            this.this_teacher_split_three2 = teacher_split_three;
            this.this_period_split_three2 = subject_split_three;
            this.this_room_split_three2 = room_split_three;
          } else {
            this.isNotSplit_three = true;
            const resultFour_three = myJson_three.split(/\r?\n/);
            console.log(resultFour_three);
            const filtered_resultThree_three = resultFour_three.filter(
              (n) => n
            );
            console.log("Final List" + filtered_resultThree_three);
            var subject_three = filtered_resultThree_three[1];
            var teacher_three = filtered_resultThree_three[0];
            var room_three = filtered_resultThree_three[2];

            //   subject = subject.replace(/(\r\n|\n|\r)/gm, "");
            this.this_teacher_three = teacher_three;
            this.this_period_three = subject_three;
            this.this_room_three = room_three;
          }
        });

      // Period Four
      // #Period Four
      //   this.this_period = localStorage.getItem("Subject");
      var retrievedObjectFour = localStorage.getItem(`PeriodFour`);
      console.log("retrievedObject: ", JSON.parse(retrievedObjectFour));
      var parsedObjectFour = JSON.parse(retrievedObjectFour);
      var subjectold_four = parsedObjectFour;
      // Get time
      // var retrievedTimeFour = localStorage.getItem("time");

      // this.this_time = retrievedTimeFour;
      //   console.log("here: " + subjectold);
      //   var subjectoldat = subjectold.replace(/(?:\r\n|\r|\n)/g, "@");
      var subjectoldatFour = subjectold_four.replace("/", "-");
      //   console.log(subjectold);

      var urlFour = `https://sostimetable-vitalik-hakim.koyeb.app/process/${subjectoldatFour}`;
      fetch(urlFour)
        .then((response_four) => {
          return response_four.json();
        })
        .then((myJson_four) => {
          //   var newParsedObject = JSON.parse(myJson);
          console.log("My" + myJson_four);
          let result_four = myJson_four.includes("&&");
          if (result_four === true) {
            let resultZero_four = myJson_four.split("&&");
            console.log(resultZero_four);
            this.isSplit_four = true;
            let resultTwo_four = resultZero_four[0];
            let resultThree_four = resultZero_four[1];
            console.log(resultTwo_four);
            console.log(resultThree_four);
            // console.log(resultTwo)
            // const resultThree = resultZero[1]
            // result two
            resultTwo_four = resultTwo_four.split(/\r?\n/);
            const filtered_resultTwo_four = resultTwo_four.filter((n) => n);
            let subject_four = filtered_resultTwo_four[1];
            let teacher_four = filtered_resultTwo_four[0];
            let room_four = filtered_resultTwo_four[2];
            this.this_teacher_split_four1 = teacher_four;
            this.this_period_split_four1 = subject_four;
            this.this_room_split_four1 = room_four;

            /// Split period
            resultThree_four = resultThree_four.split(/\r?\n/);
            const filtered_resultThree_four = resultThree_four.filter((n) => n);
            let subject_split_four = filtered_resultThree_four[1];
            let teacher_split_four = filtered_resultThree_four[0];
            let room_split_four = filtered_resultThree_four[2];
            // // result three
            // var subject = resultFour[2];
            // var teacher = resultFour[0];
            // var room = resultFour[4];
            this.this_teacher_split_four2 = teacher_split_four;
            this.this_period_split_four2 = subject_split_four;
            this.this_room_split_four2 = room_split_four;
          } else {
            this.isNotSplit_four = true;
            const resultFour_four = myJson_four.split(/\r?\n/);
            console.log(resultFour_four);
            const filtered_resultThree_four = resultFour_four.filter((n) => n);
            console.log("Final List" + filtered_resultThree_four);
            var subject_four = filtered_resultThree_four[1];
            var teacher_four = filtered_resultThree_four[0];
            var room_four = filtered_resultThree_four[2];

            //   subject = subject.replace(/(\r\n|\n|\r)/gm, "");
            this.this_teacher_four = teacher_four;
            this.this_period_four = subject_four;
            this.this_room_four = room_four;
            this.iS_Loaded = false;
            var students =
              "https://sostimetable-vitalik-hakim.koyeb.app/load/teachers";
            fetch(students)
              .then((response) => {
                return response.json();
              })
              .then((myJson) => {
                let teachers_data = myJson;
                this.teachers = teachers_data;

                localStorage.removeItem("teachers");

                window.localStorage.setItem(
                  "teachers",
                  JSON.stringify(teachers_data)
                );
                var teachers_dict = JSON.parse(
                  window.localStorage.getItem("teachers")
                );
                console.log(teachers_dict["AAS"]);
              });
          }
        });
    },
    hidebtn() {
      this.setData();
      this.iS_Loaded = false;
    },
    jqed() {
      jquery(document).ready(function () {
        jquery(".element-card").on("click", function () {
          if (jquery(this).hasClass("open")) {
            jquery(this).removeClass("open");
          } else {
            jquery(".element-card").removeClass("open");
            jquery(this).addClass("open");
          }
        });
      });
      jquery(document).ready(function () {
        jquery(".element-card-split").on("click", function () {
          if (jquery(this).hasClass("open")) {
            jquery(this).removeClass("open");
          } else {
            jquery(".element-card-split").removeClass("open");
            jquery(this).addClass("open");
          }
        });
      });
      jquery(document).ready(function () {
        jquery(".element-card-split-1").on("click", function () {
          if (jquery(this).hasClass("open")) {
            jquery(this).removeClass("open");
          } else {
            jquery(".element-card-split-1").removeClass("open");
            jquery(this).addClass("open");
          }
        });
      });
      jquery(document).ready(function () {
        jquery(".element-card-split-1-final").on("click", function () {
          if (jquery(this).hasClass("open")) {
            jquery(this).removeClass("open");
          } else {
            jquery(".element-card-split-1-final").removeClass("open");
            jquery(this).addClass("open");
          }
        });
        jquery(".element-card-split-2-final").on("click", function () {
          if (jquery(this).hasClass("open")) {
            jquery(this).removeClass("open");
          } else {
            jquery(".element-card-split-2-final").removeClass("open");
            jquery(this).addClass("open");
          }
        });
      });
    },
    jqed_reverse() {
      jquery(document).ready(function () {
        jquery(".element-card").on("click", function () {
          if (jquery(".element-card").removeClass("open")) {
            jquery(this).addClass("open");
          } else {
            jquery(this).hasClass("open");
            jquery(this).removeClass("open");
          }
        });
      });
      jquery(document).ready(function () {
        jquery(".element-card-split").on("click", function () {
          if (jquery(".element-card-split").removeClass("open")) {
            jquery(this).addClass("open");
          } else {
            jquery(this).hasClass("open");
            jquery(this).removeClass("open");
          }
        });
      });
      jquery(document).ready(function () {
        jquery(".element-card-split-1").on("click", function () {
          if (jquery(".element-card-split-1").removeClass("open")) {
            jquery(this).addClass("open");
          } else {
            jquery(this).hasClass("open");
            jquery(this).removeClass("open");
          }
        });
      });
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
  background: linear-gradient(135deg, #2980b9 0%, #9b59b6 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr="#1e5799", endColorstr="#7db9e8",GradientType=1 );
}

.container {
  position: relative;
  width: 100%;
  max-width: 960px;
  min-height: 100%;
  margin: 0px auto;
  padding: 20px;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.element-card {
  position: relative;
  width: 400px;
  height: 200px;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
  cursor: pointer;
}
.element-card:hover {
  transform: rotatey(25deg) translatex(0px) translatey(0px);
}
.element-card.open {
  width: 500px;
  height: 400px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #0e84d3;
}
.element-card .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card .front-facing .atomic-number-1 {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 18px;
  color: #000000;
}
.element-card .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 320px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  cursor: pointer;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  cursor: pointer;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card .back-facing a.btn:hover,
.element-card .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}
/* ENDS HERE: TIME FOR SPLIT */
.element-card-split {
  /* position: relative; */
  position: fixed;
  top: 150px;
  left: 290px;
  width: 400px;
  height: 100px;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
}
.element-card-split:hover {
  transform: rotatey(25deg) translatex(0px) translatey(0px);
}
.element-card-split.open {
  width: 300px;
  height: 200px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-split .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-split .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #3498db;
}
.element-card-split .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card-split .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card-split .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 25px;
  color: #000000;
}
.element-card-split .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 340px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card-split .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-split .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-split .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-split .back-facing a.btn:hover,
.element-card-split .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}

/* Card Split 2 */
.element-card-split-1 {
  /* position: ; */
  position: fixed;
  top: 300px;
  left: 290px;
  width: 400px;
  height: 100px;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
}
.element-card-split-1:hover {
  transform: rotatey(25deg) translatex(0px) translatey(0px);
}
.element-card-split-1.open {
  width: 300px;
  height: 200px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-split-1 .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-split-1 .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #3498db;
}
.element-card-split-1 .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card-split-1 .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card-split-1 .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 25px;
  color: #000000;
}
.element-card-split-1 .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 340px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card-split-1 .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-1 .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-1 .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-split-1 .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-split-1 .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-split-1 .back-facing a.btn:hover,
.element-card-split-1 .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}

.suppoprt-me {
  display: inline-block;
  position: fixed;
  bottom: 10px;
  left: 10px;
  width: 15vw;
  max-width: 100px;
  min-width: 100px;
  z-index: 9;
}
.suppoprt-me img {
  width: 100%;
  height: auto;
}
h4 {
  display: block;
  /* margin-top: 1.33em; */
  /* margin-bottom: 1.33em; */
  margin-left: 0;
  margin-right: 0;
  font-weight: bold;
  color: rgb(130, 20, 220);
}
h3 {
  display: block;
  margin-top: 1em;
  margin-bottom: 0em;
  margin-left: 0;
  margin-right: 0;
  font-weight: bold;
  color: crimson;
}
.status-circle {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: rgb(14, 221, 83);
  border: 2px solid white;
  bottom: 0;
  right: 100;
  top: 0%;
  position: fixed;
}
.status-circle-red {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: orange;
  border: 2px solid white;
  bottom: 0;
  right: 100;
  top: 0%;
  position: fixed;
}
.status-circle-loading {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: rgb(14, 221, 83);
  border: 2px solid white;
  bottom: 0;
  right: 95%;
  top: 0%;
  position: fixed;
}
.status-circle-yellow-loading {
  position: fixed;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: rgb(255, 238, 0);
  border: 2px solid white;
  bottom: 0;
  right: 89%;
  top: 0%;
}
.status-circle-red-loading {
  position: fixed;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: rgb(255, 60, 0);
  border: 2px solid white;
  bottom: 0;
  right: 82%;
  top: 0%;
}

.element-card-loading {
  position: absolute;
  top: 200px;
  left: 290px;
  width: 400px;
  height: 100px;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
  cursor: pointer;
}
.element-card-loading:hover {
  transform: rotatey(45deg) translatex(0px) translatey(0px);
}
.element-card-loading.open {
  width: 300px;
  height: 200px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-loading .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-loading .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 42px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #3498db;
}
.element-card-loading .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 12px;
  margin: 15px 0 0 0;
  text-align: center;
  color: #3498db;
}
.element-card-loading .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 12px;
  color: #2980b9;
}
.element-card-loading .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 12px;
  color: #2980b9;
}
.element-card-loading .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-loading .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-loading .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-loading .back-facing a.btn:hover,
.element-card-loading .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}

/* Splits style */
.element-card-split-2-final {
  position: fixed;
  width: 190px;
  height: 169px;
  left: 0%;
  top: 0%;
  right: 0;
  bottom: 0;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
  /* margin-left: 2; */

  cursor: pointer;
}
.element-card-split-2-final:hover {
  transform: rotatey(10deg) translatex(0px) translatey(0px);
}
.element-card-split-2-final.open {
  width: 200px;
  height: 200px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-split-2-final .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-split-2-final .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #0e84d3;
}
.element-card-split-2-final .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card-split-2-final .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card-split-2-final .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 18px;
  color: #000000;
}
.element-card-split-2-final .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 340px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card-split-2-final .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-2-final .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-2-final .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-split-2-final .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-split-2-final .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-split-2-final .back-facing a.btn:hover,
.element-card-split-2-final .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}
/* Split two */
.element-card-split-1-final {
  position: fixed;
  width: 190px;
  height: 169px;
  left: 50%;
  top: 0%;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
  /* margin-left: 2; */

  cursor: pointer;
}
.element-card-split-1-final:hover {
  transform: rotatey(10deg) translatex(0px) translatey(0px);
}
.element-card-split-1-final.open {
  width: 200px;
  height: 200px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-split-1-final .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-split-1-final .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #0e84d3;
}
.element-card-split-1-final .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card-split-1-final .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card-split-1-final .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 18px;
  color: #000000;
}
.element-card-split-1-final .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 340px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card-split-1-final .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-1-final .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-1-final .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-split-1-final .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-split-1-final .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-split-1-final .back-facing a.btn:hover,
.element-card-split-1-final .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}

/* Main card */
.element-card-split-container {
  position: relative;
  width: 455px;
  height: 220px;
  transform-style: preserve-3d;
  transform: rotatey(0deg) translatex(0px) translatey(0px);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.4);
  margin: 20px;
  border-radius: 5px;
  cursor: pointer;
}
.element-card-split-container:hover {
  transform: rotatey(10deg) translatex(0px) translatey(0px);
}
.element-card-split-container.open {
  width: 500px;
  height: 400px;
  transform: rotatey(-180deg) translatex(0px) translatey(0px);
}
.element-card-split-container .front-facing {
  transform: rotateY(0deg) translateZ(2px);
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
}
.element-card-split-2-final-container .front-facing .abr {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 20px;
  margin: -35px 0 0 0;
  text-align: center;
  color: #0e84d3;
}
.element-card-split-2-final-container .front-facing .title {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 0;
  text-transform: uppercase;
  font-size: 15px;
  margin: 15px 0 0 0;
  text-align: center;
  color: rgb(209, 66, 209);
}
.element-card-split-2-final-container .front-facing .atomic-number {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  color: crimson;
}
.element-card-split-2-final-container .front-facing .atomic-mass {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 18px;
  color: #000000;
}
.element-card-split-2-final-container .front-facing .atomic-mass-1 {
  position: absolute;
  bottom: 10px;
  right: 340px;
  font-size: 18px;
  color: #2e0fdd;
}
.element-card-split-2-final-container .front-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 135px;
  font-size: 12px;
  color: #2980b9;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-2-final-container .back-facing .flip-btn {
  position: absolute;
  bottom: 10px;
  right: 190px;
  font-size: 12px;
  color: #2980b9;
  background-color: crimson; /* red */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 5px;
  font-size: 16px;
}
.element-card-split-2-final-container .back-facing {
  transform: rotateY(180deg) translateZ(0px);
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #ecf0f1;
  border: 2px white solid;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  overflow: hidden;
}
.element-card-split-2-final-container .back-facing p {
  font-size: 14px;
  margin: 0;
}
.element-card-split-2-final-container .back-facing a.btn {
  display: inline-block;
  background-color: white;
  padding: 5px 15px;
  margin: 20px 0 0 0;
  color: #eee;
  background-color: #3498db;
  text-decoration: none;
  border-radius: 3px;
}
.element-card-split-2-final-container .back-facing a.btn:hover,
.element-card-split-2-final-container .back-facing a.btn:focus {
  color: #fff;
  background-color: #2980b9;
}
/* The Loading Modal (background) */
.modal-loading {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}
/* Modal Content */
.modal-content-loading {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}
.img-tg {
  border-radius: 50%;
}
button {
  background-color: #21c900;
  border: none;
  color: #ffffff;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button-timetable {
  background-color: #21c900;
  border: none;
  position: fixed;
  color: #ffffff;
  top: 45.5%;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button-2 {
  background-color: red;
  border: none;
  color: #ffffff;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
.button-3 {
  background-color: #009df8;
  border: none;
  color: #ffffff;
  font-size: 15px;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 4px;
  outline: none;
}
</style>
