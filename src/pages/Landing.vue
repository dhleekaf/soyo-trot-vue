<template>
  <div>
    <div class="page-header page-header-small">
      <parallax
        class="page-header-image"
        style="background-image: url('img/mister_trot.jpg')"
      >
      </parallax>
      <div class="content-center">
        <div class="container">
          <h1 class="title">내일의 眞 善 美</h1>
        </div>
      </div>
    </div>
    <div class="section section-about-us">
      <div class="container">
        <div class="row">
          <div class="col-md-8 ml-auto mr-auto text-center">
            <h4 class="title">
              예측해보기:
              <div>
                <select
                  v-model="program"
                  v-on:input="
                    updatePrediction(
                      $event.target.value,
                      $event.target.selectedIndex
                    )
                  "
                >
                  <option disabled :value="null">프로그램 선택</option>
                  <option
                    v-for="(item, index) in items"
                    :value="item"
                    :key="index"
                  >
                    {{ item }}
                  </option>
                </select>
              </div>
            </h4>
          </div>
        </div>
        <div class="separator separator-primary"></div>
        <div class="section section-team text-center">
          <div class="container" v-show="predicted">
            <h2 class="title">{{ program }} 예측결과</h2>
            <div class="team">
              <div class="row">
                <div
                  class="col-md-4"
                  v-for="singer in results[this.selected_idx]"
                  :key="singer.name"
                >
                  <div class="team-player">
                    <h3>{{ singer.rank }}</h3>
                    <img
                      :src="singer.src"
                      :alt="singer.name"
                      class="rounded-circle img-fluid img-raised"
                    />
                    <h4 class="title">{{ singer.name }}</h4>
                    <p class="category text-primary">{{ singer.subtitle }}</p>
                    <p class="description">
                      You can write here details about one of your team members.
                      You can give more details about what they do. Feel free to
                      add some <a href="#">links</a> for people to be able to
                      follow them outside the site.
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="section section-team text-center">
      <div class="container" v-show="false">
        <h2 class="title">후보들?</h2>
        <div class="team">
          <div class="row">
            <div class="col-md-4">
              <div class="team-player">
                <h3>眞</h3>
                <img
                  src="img/avatar.jpg"
                  alt="Thumbnail Image"
                  class="rounded-circle img-fluid img-raised"
                />
                <h4 class="title">Romina Hadid</h4>
                <p class="category text-primary">Model</p>
                <p class="description">
                  You can write here details about one of your team members. You
                  can give more details about what they do. Feel free to add
                  some <a href="#">links</a> for people to be able to follow
                  them outside the site.
                </p>
                <!-- <a href="#pablo" class="btn btn-primary btn-icon btn-round"
                  ><i class="fab fa-twitter"></i
                ></a>
                <a href="#pablo" class="btn btn-primary btn-icon btn-round"
                  ><i class="fab fa-instagram"></i
                ></a> -->
              </div>
            </div>
            <div class="col-md-4">
              <div class="team-player">
                <h3>善</h3>
                <img
                  src="img/ryan.jpg"
                  alt="Thumbnail Image"
                  class="rounded-circle img-fluid img-raised"
                />
                <h4 class="title">Ryan Tompson</h4>
                <p class="category text-primary">Designer</p>
                <p class="description">
                  You can write here details about one of your team members. You
                  can give more details about what they do. Feel free to add
                  some <a href="#">links</a> for people to be able to follow
                  them outside the site.
                </p>
              </div>
            </div>
            <div class="col-md-4">
              <div class="team-player">
                <h3>美</h3>
                <img
                  src="img/eva.jpg"
                  alt="Thumbnail Image"
                  class="rounded-circle img-fluid img-raised"
                />
                <h4 class="title">Eva Jenner</h4>
                <p class="category text-primary">Fashion</p>
                <p class="description">
                  You can write here details about one of your team members. You
                  can give more details about what they do. Feel free to add
                  some <a href="#">links</a> for people to be able to follow
                  them outside the site.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Button, FormGroupInput } from "@/components";
export default {
  name: "landing",
  bodyClass: "landing-page",
  components: {
    [Button.name]: Button,
    [FormGroupInput.name]: FormGroupInput,
  },
  data() {
    return {
      form: {
        firstName: "",
        email: "",
        message: "",
      },
      program: null,
      items: ["내일은 미스트롯2", "트롯 전국체전"],
      predicted: false,
      results: [
        [
          {
            rank: "眞",
            name: "김태연",
            src: "img/김태연.jpg",
            subtitle: "2012년 4월생 전북 부안",
            desc: "",
          },
          {
            rank: "善",
            name: "홍지윤",
            src: "img/홍지윤.jpg",
            subtitle: "1995년 3월생 전남 장흥",
            desc: "",
          },
          {
            rank: "美",
            name: "김다현",
            src: "img/김다현.jpg",
            subtitle: "2009년 2월생 충북",
            desc: "",
          },
        ],
        [],
      ],
      selected_idx: 1,
    };
  },
  // props: ["value", "items", "input_id"],
  created() {},
  methods: {
    updatePrediction: function (value, idx) {
      // this.$emit("input", value);
      this.selected_idx = idx - 1;
      this.predicted = true;
    },
  },
};
</script>
<style></style>
