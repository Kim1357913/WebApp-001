<script setup>
import { ref, reactive, computed } from "vue";
import charaNad09Img from "../assets/Char-Nad-09/Char.webp";
import autoIcon from "../assets/Char-Nad-09/Bow_Geo.webp";
import skill1Icon from "../assets/Char-Nad-09/Talent_Countermeasure-_Lumi21.webp";
import skill2Icon from "../assets/Char-Nad-09/Talent_Memo-_Survival_Guide_in_Extreme_Conditions.webp";
import talent1Icon from "../assets/Char-Nad-09/Talent_Field_Observation_Notes.webp";
import Charactor from "./Char-Nad-09.vue";
import demoGrid from "./Grid.vue";
import calcDmg from "./CalcDmg.vue";
const isHovered = ref(false);
const mouseOverAction = () => {
  isHovered.value = true;
};
const mouseOutAction = () => {
  isHovered.value = false;
};
const isOpen = ref(false);

const damages = [
  { name: "キャラクター1", value: 1200, color: "#e76f51" },
  { name: "キャラクター2", value: 900, color: "#2a9d8f" },
  { name: "キャラクター3", value: 700, color: "#e9c46a" },
  { name: "キャラクター4", value: 500, color: "#457b9d" },
];
const totalDamage = computed(() => damages.reduce((sum, character) => sum + character.value, 0));//reduceは配列を1つの値にまとめる
const maxDamage = computed(() => Math.max(...damages.map((character) => character.value)));//mathは数値、mapは新しい配列を作る
const pieStyle = computed(() => {
  let start = 0;
  const sections = damages.map((character) => {
    const end = start + (character.value / totalDamage.value) * 100;
    const section = `${character.color} ${start}% ${end}%`;
    start = end;
    return section;
  });
  return { background: `conic-gradient(${sections.join(", ")})` };
});
</script>

<template>
  <section id="top-steps">
    <div class="hero">
      <img :src="charaNad09Img" class="base" width="718" height="440" alt="" />
    </div>
    <ul>
      <a @mouseover="mouseOverAction" @mouseout="mouseOutAction">
        <li>
          <img :src="autoIcon" class="top-icon" role="presentation" aria-hidden="true" />
          <div class="skillExplain1" v-if="isHovered"><Charactor /></div>
        </li>
      </a>
      <a>
        <li>
          <img :src="skill1Icon" class="top-icon" role="presentation" aria-hidden="true" />
        </li>
      </a>
      <a>
        <li>
          <img :src="skill2Icon" class="top-icon" role="presentation" aria-hidden="true" />
        </li>
      </a>
    </ul>
  </section>
  <div class="ticks"></div>

  <section id="next-steps">
    <div id="docs">
      <div class="mb-1 grid grid-cols-4">
        <div class="flex-auto text-center bg-[#3a7e93] border border-[#060d0f] py-2">"tab1"</div>
        <div class="flex-auto text-center bg-[#3a7e93] border border-[#060d0f] py-2">"tab2"</div>
        <div class="flex-auto text-center bg-[#3a7e93] border border-[#060d0f] py-2">"tab3"</div>
        <div class="flex-auto text-center bg-[#3a7e93] border border-[#060d0f] py-2">"tab4"</div>
      </div>
      <div class="mb-2 border border-[#333333] bg-gradient-to-r from-[#010102cc] to-[#222222cc] py-2">
        <div class="flex justify-between flex-wrap">
          <div class="flex md:basis-1/2 sm:block">
            <div class="sm:block">
              <div>PTバフ</div>
              <div class="flex gap-2 justify-center" >
                <img :src="autoIcon" class="top-icon" width="40" height="40" />
                <img :src="autoIcon" class="top-icon" width="40" height="40" />
              </div>
            </div>
            <div>
              <div>武器</div>
              <img :src="autoIcon" class="top-icon" width="40" height="40" />
            </div>
            <div class="flex justify-center gap-2">
              <div>Lv:90</div>
              <div>天賦Lv:10</div>
            </div>
          </div>
          <div class=" md:basis-1/2">
            <img :src="autoIcon" class="top-icon" width="40" height="40" />
            <calcDmg />
          </div>
        </div>
      </div>
      <div class="damage-charts">
        <h2>キャラクター別ダメージ</h2>
        <p>合計ダメージ: {{ totalDamage }}</p>

        <div class="chart-layout">
          <div class="bar-chart" aria-label="棒グラフ">
            <div v-for="character in damages" :key="character.name" class="bar-row">
              <span class="character-name">{{ character.name }}</span>
              <div class="bar-background">
                <div
                  class="bar"
                  :style="{ width: `${(character.value / maxDamage) * 100}%`, backgroundColor: character.color }"
                ></div>
              </div>
              <strong>{{ character.value }}</strong>
            </div>
          </div>

          <div class="pie-area">
            <div class="pie-chart" :style="pieStyle" aria-label="円グラフ"></div>
            <ul>
              <li v-for="character in damages" :key="character.name">
                <span class="color-dot" :style="{ backgroundColor: character.color }"></span>
                {{ character.name }}: {{ ((character.value / totalDamage) * 100).toFixed(1) }}%
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="area">
        <input type="radio" name="tab_name" id="tab1" checked />
        <label class="tab_class" for="tab1">タブ1</label>
        <div class="content_class">
          <p>タブ1のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab2" />
        <label class="tab_class" for="tab2">タブ2</label>
        <div class="content_class">
          <p>タブ2のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab3" />
        <label class="tab_class" for="tab3">タブ3</label>
        <div class="content_class">
          <p>タブ3のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab4" />
        <label class="tab_class" for="tab4">タブ4</label>
        <div class="content_class">
          <p>タブ4のコンテンツを表示します</p>
        </div>
      </div>

      <svg class="icon" role="presentation" aria-hidden="true">
        <use href="/icons.svg#documentation-icon"></use>
      </svg>
      <h2>Documentation</h2>
      <p>Your questions, answered</p>
      <ul>
        <li>
          <a href="https://vite.dev/" target="_blank">
            <img class="logo" :src="viteLogo" alt="" />
            Explore Vitex
          </a>
        </li>
        <li>
          <a href="https://vuejs.org/" target="_blank">
            <img class="button-icon" :src="vueLogo" alt="" />
            Learn more
          </a>
        </li>
      </ul>
    </div>
    <div id="social">
      <CalcDmg />
      <svg class="icon" role="presentation" aria-hidden="true">
        <use href="/icons.svg#social-icon"></use>
      </svg>
      <h2>Connect with us</h2>
      <p>Join the Vite community</p>
      <ul>
        <li>
          <a href="https://github.com/vitejs/vite" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#github-icon"></use>
            </svg>
            GitHub
          </a>
        </li>
        <li>
          <a href="https://chat.vite.dev/" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#discord-icon"></use>
            </svg>
            Discord
          </a>
        </li>
        <li>
          <a href="https://x.com/vite_js" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#x-icon"></use>
            </svg>
            X.com
          </a>
        </li>
        <li>
          <a href="https://bsky.app/profile/vite.dev" target="_blank">
            <svg class="button-icon" role="presentation" aria-hidden="true">
              <use href="/icons.svg#bluesky-icon"></use>
            </svg>
            Bluesky
          </a>
        </li>
      </ul>
    </div>
  </section>

  <div class="ticks"></div>
  <section id="spacer"></section>
</template>
