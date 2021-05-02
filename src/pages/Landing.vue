<template>
  <div>
    <div class="page-header page-header-small">
      <li
        v-for="(paral, index) in parallaxList"
        :key="index"
        :class="{ off: index !== paral_cur_idx }"
      >
        <parallax
          class="page-header-image"
          :style="'background-image: url(' + paral.src + ')'"
        >
        </parallax>
      </li>
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
                    <p>{{ singer.birth }}</p>
                    <p
                      class="category text-primary"
                      v-if="singer.subtitle.length > 0"
                    >
                      실제 순위 : {{ program }} {{ singer.subtitle }}
                    </p>
                    <p class="description" v-if="singer.desc">
                      {{ singer.desc }}
                    </p>
                    <p class="description" v-else v-html="singer.html"></p>
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

let timer = null;
const AUTO_INTERVAL = 5000;

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
      parallaxList: [
        { src: "img/mister_trot.jpg" },
        { src: "img/miss_trot.jpg" },
        { src: "img/miss_trot2_1.jpg" },
        { src: "img/miss_trot2_2.jpg" },
      ],
      paral_cur_idx: 0,
      program: null,
      items: ["내일은 미스트롯2", "트롯 전국체전"],
      predicted: false,
      results: [
        [
          {
            rank: "眞",
            name: "김태연",
            src: "img/김태연.jpg",
            birth: "2012년 4월 전북 부안",
            subtitle: "4위",
            desc:
              "4세에 판소리, 민요를 시작한 이후 대한민국 춘향국악대전 최연소 대상 등 여러 상을 수상한 ‘판소리계 신동’이며, 미국 케네디 센터와 카네기 홀에서 공연을 펼쳐 전세계에 국악을 널리 알리기도 했다.",
            html: null,
          },
          {
            rank: "善",
            name: "홍지윤",
            src: "img/홍지윤.jpg",
            birth: "1995년 3월 전남 장흥",
            subtitle: "善",
            desc:
              "춘 엔터테인먼트의 연습생 출신으로, 여동생 홍주현과 함께 믹스나인에 참가하여 장윤정의 짠짜라를 불렀다. 그러나 다리 부상으로 연습생 생활을 마감하고 트롯 가수의 길을 걷게 됐다.",
            html: null,
          },
          {
            rank: "美",
            name: "김다현",
            src: "img/김다현.jpg",
            birth: "2009년 2월 충북",
            subtitle: "美",
            desc:
              "2020년 9월 25일 《꽃처녀》로 음반 데뷔했으며 주요 대표곡은 '꽃처녀', '파이팅'이다. ",
            html: null,
          },
        ],
        [
          {
            rank: "眞",
            name: "진해성",
            src: "img/진해성.jpg",
            birth: "1990년 6월 부산",
            subtitle: "眞",
            desc:
              "데뷔는 2012년에 했지만, 실제 주목받기 시작한 시기는 여러 예능 프로그램에 출연하기 시작한 2018년부터다. 전직 유도선수 출신.",
            html: null,
          },
          {
            rank: "善",
            name: "재하",
            src: "img/재하.jpg",
            birth: "1993년 11월 미국",
            subtitle: "善",
            desc:
              "어머니가 립스틱 짙게 바르고라는 노래로 유명한 가수 임주리다. 트롯 전국체전에서 어머니의 곡을 불렀다. 이후 갈라쇼에서 어머니와 무대를 꾸몄다.",
            html: null,
          },
          {
            rank: "美",
            name: "오유진",
            src: "img/오유진.jpg",
            birth: "2010년 경남 진주",
            subtitle: "美",
            desc:
              "트롯을 좋아하는 외할머니를 따라 노래교실을 다니며 트로트에 빠졌다.",
            html: null,
          },
          {
            rank: "후보",
            name: "신승태",
            src: "img/신승태.jpg",
            birth: "1986년 11월",
            subtitle: "4위",
            desc: "",
            html:
              "대한민국 국악인이자 가수. <a href='https://ko.wikipedia.org/wiki/%EC%8B%A0%EC%8A%B9%ED%83%9C'>수상이력</a>",
          },
          {
            rank: "후보",
            name: "최향",
            src: "img/최향.jpg",
            birth: "1995년 6월 전북 익산",
            subtitle: "7위",
            desc:
              "2017년 부터 국내 각종 가요제에 참가해 '음색깡패'라 불리며 상만 20개를 쓸어담은 괴기한 이력의 소유자다. 트로트, 알앤비, 힙합, 국악, 재즈 등 다양한 장르를 부른다.",
            html: null,
          },
        ],
      ],
      selected_idx: 1,
    };
  },
  // props: ["value", "items", "input_id"],
  created() {},
  mounted() {
    this.setAutoRoll();
  },
  methods: {
    updatePrediction: function (value, idx) {
      // this.$emit("input", value);
      this.selected_idx = idx - 1;
      this.predicted = true;
    },
    setAutoRoll() {
      let vueSelf = this;
      timer = setInterval(function () {
        vueSelf.addIndex();
      }, AUTO_INTERVAL);
    },
    addIndex() {
      let new_index = this.paral_cur_idx + 1;
      this.paral_cur_idx =
        new_index === this.parallaxList.length ? 0 : new_index;
    },
  },
};
</script>
<style></style>
