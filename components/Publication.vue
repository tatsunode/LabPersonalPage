<template>
  <section>
    <h1 class="title section-title">Publications / 業績</h1>
    <section class="subsection container">
      <h2 class="subtitle">Journals・Magazines / 論文誌等</h2>
      <ol>
        <li v-for="paper in sortedJornals" :key="paper.title">
          <paper-list-item :paper="paper" />
        </li>
      </ol>
    </section>
    <section class="subsection container">
      <h2 class="subtitle">
        International Conferences / 国際会議（Full Paper）
      </h2>
      <ol>
        <li v-for="paper in sortedInternationalConfs" :key="paper.title">
          <paper-list-item :paper="paper" />
        </li>
      </ol>
    </section>
    <section class="subsection container">
      <h2 class="subtitle">
        International Conferences / 国際会議（Demo・Poster）
      </h2>
      <ol>
        <li
          v-for="paper in sortedInternationalConfsPosterDemo"
          :key="paper.title"
        >
          <paper-list-item :paper="paper" />
        </li>
      </ol>
    </section>
    <section class="subsection container">
      <h2 class="subtitle">Japanese Domestic Conferences / 国内研究会等</h2>
      <ol>
        <li v-for="paper in sortedDomesticConfs" :key="paper.title">
          <paper-list-item :paper="paper" />
        </li>
      </ol>
    </section>
    <section class="subsection container">
      <h2 class="subtitle">Thesis / 学位論文</h2>
      <ol>
        <li v-for="paper in sortedThesis" :key="paper.title">
          <paper-list-item :paper="paper" />
        </li>
      </ol>
    </section>
  </section>
</template>

<script>
import publications from "static/publications.json";
import PaperListItem from "~/components/PaperListItem.vue";

function sortByDate(list) {
  return list.sort(function (a, b) {
    if (a.datetime < b.datetime) return 1;
    if (a.datetime > b.datetime) return -1;
    return 0;
  });
}

export default {
  data: function () {
    return {
      jornals: publications.jornals,
      internationalConfs: [],
      internationalConfsPosterDemo: [],
      domesticConfs: publications.domestic_conferences,
      thesis: publications.thesis,
    };
  },
  created: function () {
    this.internationalConfs = publications.international_conferences.filter(
      function (item) {
        return item.presentation_type == "oral";
      }
    );
    this.internationalConfsPosterDemo = publications.international_conferences.filter(
      function (item) {
        return item.presentation_type != "oral";
      }
    );
  },
  computed: {
    sortedJornals: function () {
      return sortByDate(this.jornals.slice());
    },
    sortedInternationalConfs: function () {
      return sortByDate(this.internationalConfs.slice());
    },
    sortedInternationalConfsPosterDemo: function () {
      return sortByDate(this.internationalConfsPosterDemo.slice());
    },
    sortedDomesticConfs: function () {
      return sortByDate(this.domesticConfs.slice());
    },
    sortedThesis: function () {
      return sortByDate(this.thesis.slice());
    },
  },
  components: {
    PaperListItem,
  },
};
</script>