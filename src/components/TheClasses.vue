<template>
  <div id="TheClasses" class="TheClasses">
    <div class="container">
      <div class="main_title">الفرق الدراسية</div>
      <v-card class="mx-auto" width="100%" style="padding: 20px 10px">
        <v-card-title
          style="padding: 10px"
          class="text-h6 font-weight-regular justify-space-between mb-2.5"
        >
          <v-avatar v-text="step"></v-avatar>
          <span
            style="font-size: 20px; font-weight: bold; font-family: system-ui"
            >{{ currentTitle }}</span
          >
        </v-card-title>

        <v-window v-model="step">
          <v-window-item :value="1">
            <div
              class="selecte_1 flex justify-center gap-2.5 flex-wrap selecte"
            >
              <span
                class="border-gray-300 border rounded flex justify-center items-center p-10 cursor-pointer hover_color_border"
                @click="select_1"
                >كلية الشريعة و القانون</span
              >
              <span
                class="border-gray-300 border rounded flex justify-center items-center p-10 cursor-pointer hover_color_border"
                @click="select_1"
                >معهد أعوان القضاء</span
              >
            </div>
          </v-window-item>

          <v-window-item :value="2">
            <div
              class="selecte_2 flex justify-center gap-2.5 flex-wrap selecte"
            >
              <span
                @click="select_2"
                class="border-gray-300 border rounded flex justify-center items-center p-10 cursor-pointer hover_color_border"
                >عربي</span
              >
              <span
                @click="select_2"
                class="border-gray-300 border rounded flex justify-center items-center p-10 cursor-pointer hover_color_border"
                >English</span
              >
            </div>
          </v-window-item>

          <v-window-item :value="3">
            <div class="selecte_3 flex justify-center gap-2.5 flex-wrap">
              <router-link
                to="/Main_Class"
                v-for="Class in classes"
                :key="Class"
                class="border-gray-300 border rounded flex justify-center items-center w-23 p-10 cursor-pointer hover_color_border"
              >
                {{ Class }}
              </router-link>
            </div>
          </v-window-item>
        </v-window>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn
            v-if="step > 1"
            variant="text"
            @click="step--"
            style="
              color: var(--main-color);
              border: 1px solid var(--main-color);
            "
          >
            السابق
          </v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </div>
  </div>
</template>
<script>
export default {
  name: "TheClasses",
  mounted() {
    this.select();
  },
  data() {
    return {
      type: "",
      lang: "",
      class: "",
      classes: [
        "الفرقة الأولي",
        "الفرقة الثانية",
        "الفرقة الثالثة",
        "الفرقة الرابعة",
      ],
      step: 1,
    };
  },
  computed: {
    currentTitle() {
      switch (this.step) {
        case 1:
          return "الدراسة";
        case 2:
          return "القسم";
        default:
          return "الفرقة";
      }
    },
  },
  methods: {
    select_1() {
      this.step++;
      setTimeout(() => {
        if (this.type === "معهد أعوان القضاء") {
          document.querySelector(".selecte_2 > span:last-child").style.display =
            "none";
        } else {
          document.querySelector(".selecte_2 > span:last-child").style.display =
            "block";
        }
        document.querySelectorAll(".selecte_2 span").forEach((e) => {
          e.onclick = () => {
            this.lang = e.innerHTML;
          };
        });
      }, 1);
    },
    select_2() {
      this.step++;
      setTimeout(() => {
        if (this.type === "معهد أعوان القضاء") {
          document.querySelector(
            ".selecte_3  > a:nth-child(3) "
          ).style.display = "none";
          document.querySelector(
            ".selecte_3  > a:nth-child(4) "
          ).style.display = "none";
        } else {
          document.querySelector(
            ".selecte_3  > a:nth-child(3) "
          ).style.display = "block";
          document.querySelector(
            ".selecte_3  > a:nth-child(4) "
          ).style.display = "block";
        }
        document.querySelectorAll(".selecte_3 a").forEach((e) => {
          e.onclick = () => {
            this.class = e.innerHTML;
            localStorage.setItem("updateType", this.type);
            localStorage.setItem("updateLang", this.lang);
            localStorage.setItem("updateClass", this.class);
          };
        });
      }, 2);
    },
    select() {
      document.querySelectorAll(".selecte_1 span").forEach((e) => {
        e.onclick = () => {
          this.type = e.innerHTML;
        };
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.v-avatar.v-avatar--density-default {
  width: 30px;
  height: 30px;
  border-radius: 5px;
  background: var(--main-color) !important;
  color: #fff;
}
.v-card-title {
  display: flex;
  justify-content: flex-start !important;
  align-items: center;
  gap: 10px;
}
.selecte {
  & > span {
    color: var(--main-color);
    font-weight: bold;
    font-size: 16px;
    width: 46% !important;
    font-family: system-ui;
    text-align: center;
  }
}
.selecte_3 > a {
  color: var(--main-color) !important;
  font-weight: bold;
  font-size: 16px;
  width: 46% !important;
  font-family: system-ui;
  text-align: center;
}
@media (min-width: 1200px) {
}

@media (min-width: 768px) and (max-width: 1199px) {
}

@media (max-width: 767px) {
  .selecte_1,
  .selecte_2,
  .selecte_3 {
    flex-direction: column;
    span {
      width: 95% !important;
      margin: auto;
    }
  }
  .selecte_3 > a {
    width: 95% !important;
    margin: auto;
  }
}
</style>
