<template>
  <div class="free" @mouseenter="getFreeClass">
    <!-- Button trigger modal -->
    <button
      id="button-free"
      type="button"
      class="inline-block px-6 py-3.5 bg-green-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-green-600 hover:shadow-lg focus:bg-green-600 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-green-700 active:shadow-lg transition duration-150 ease-in-out"
      data-bs-toggle="modal"
      data-bs-target="#exampleModal"
    >
      Free ClassRooms
    </button>

    <!-- Modal -->
    <div
      class="modal"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-fullscreen">
        <div class="modal-content">
          <div class="modal-header">
            <h5
              class="modal-title text-red-500 text-xl font-medium mb-2"
              id="exampleModalLabel"
            >
              Free ClassRooms Right Now
            </h5>

            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="modal-body relative p-4">
              <!-- Render Cards Here -->
              <div class="grid grid-cols-4 gap-4">
                <div
                  v-for="product in classfree"
                  class="product-item"
                  v-bind:key="product.id"
                >
                  <div
                    class="block rounded-lg shadow-lg bg-white max-w-sm text-center"
                    @mouseenter="get_key(product)"
                  >
                    <div class="py-3 px-6 border-b border-gray-300"></div>
                    <div class="p-6">
                      <h5 class="text-red-500 text-xl font-medium mb-2">
                        {{ product }}
                      </h5>
                      <p
                        class="text-blue-600 text-base mb-4"
                        v-if="
                          this.period_time_db[
                            this.estimated_periods[product]
                          ] == ''
                        "
                      >
                        Free until school ends
                      </p>
                      <p
                        class="text-blue-600 text-base mb-4"
                        v-if="
                          this.period_time_db[
                            this.estimated_periods[product]
                          ] != ''
                        "
                      >
                        {{ this.free }}
                        {{
                          this.period_time_db[this.estimated_periods[product]]
                        }}
                      </p>

                      <!-- for {{this.estimated_periods[product]}} periods -->
                    </div>
                    <div
                      class="py-3 px-6 border-t border-gray-300 text-green-600"
                    >
                      <a :href="classkeys">View full Class timetable</a>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Bossman down here -->
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-danger"
              data-bs-dismiss="modal"
            >
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FreeClasses",
  components: {},
  data() {
    return {
      url_base: "https://sostimetable-vitalik-hakim.koyeb.app/search/",
      Classes: "",
      classfree: [],
      links: {
        "artroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/artroom1.png",
        "audiovisualroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/audiovisualroom1.png",
        "audiovisualroom2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/audiovisualroom2.png",
        "biologylab.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/biologylab.png",
        "casroom.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/casroom.png",
        "chemistrylab.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/chemistrylab.png",
        "englishroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/englishroom1.png",
        "englishroom2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/englishroom2.png",
        "englishroom3.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/englishroom3.png",
        "englishroom4.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/englishroom4.png",
        "generallab.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/generallab.png",
        "generalroom.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/generalroom.png",
        "humanitiesroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/humanitiesroom1.png",
        "humanitiesroom2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/humanitiesroom2.png",
        "humanitiesroom3.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/humanitiesroom3.png",
        "itlaboratory1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/itlaboratory1.png",
        "itlaboratory2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/itlaboratory2.png",
        "maclab.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/maclab.png",
        "margaretnkrumahhall.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/margaretnkrumahhall.png",
        "mathroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/mathroom1.png",
        "mathroom2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/mathroom2.png",
        "mathroom3.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/mathroom3.png",
        "mathroom4.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/mathroom4.png",
        "modernlanguagesroom1.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/modernlanguagesroom1.png",
        "modernlanguagesroom2.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/modernlanguagesroom2.png",
        "modernlanguagesroom3.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/modernlanguagesroom3.png",
        "modernlanguagesroom4.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/modernlanguagesroom4.png",
        "musicroom.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/musicroom.png",
        "performingartsroom.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/performingartsroom.png",
        "physicslab.png":
          "https://raw.githubusercontent.com/vitalik-hakim/TABLES404/main/imgs/physicslab.png",
      },
      classkeys: [],
      estimated_periods: {},
      period_time_db: {},
      free: "Free until: ",
      Period: false,
    };
  },
  watch: {},
  methods: {
    getFreeClass() {
      var Classes = "https://sostimetable-vitalik-hakim.koyeb.app/free-classes";
      fetch(Classes)
        .then((response) => {
          return response.json();
        })
        .then((myJson) => {
          // console.log(myJson);
          let FreeClasses = myJson;
          this.Classes = FreeClasses;
          localStorage.removeItem("FREE-CLASSES");
          localStorage.setItem("FREE-CLASSES", JSON.stringify(FreeClasses));
          var retrieved_classes = JSON.parse(
            localStorage.getItem("FREE-CLASSES")
          );
          let Final_Classes = retrieved_classes;
          this.classfree = Final_Classes[0];
          this.estimated_periods = Final_Classes[1];
          this.period_time_db = Final_Classes[2];
          return Final_Classes;
        });
    },
    get_key(retrieved_class) {
      var lower = retrieved_class.replace(/\s/g, "");
      lower = lower.toLowerCase() + ".png";
      this.classkeys = this.links[lower];
    },
  },
};
</script>

<style>
#button-free {
  position: fixed;
  left: 60.5%;
  top: 33.5%;
}

#h5 {
  color: crimson;
  text-align: center;
}
h5 {
  color: crimson;
}
.modal-footer.custom-height {
  height: 80px;
}
</style>
