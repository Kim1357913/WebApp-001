<script setup>
import { ref, reactive, computed } from "vue";
import charaNad09Img from "../assets/Char-Nad-09/Char.webp";
import autoIcon from "../assets/Char-Nad-09/Bow_Geo.webp";
import skill1Icon from "../assets/Char-Nad-09/Talent_Countermeasure-_Lumi21.webp";
import skill2Icon from "../assets/Char-Nad-09/Talent_Memo-_Survival_Guide_in_Extreme_Conditions.webp";
import Charactor from "./Char-Nad-09.vue";
import calcDmg from "./CalcDmg.vue";
import { characters } from "../data/characters.js";
import { weapons } from "../data/weapons.js";
const isHovered = ref(false);
const mouseOverAction = () => {
  isHovered.value = true;
};
const mouseOutAction = () => {
  isHovered.value = false;
};
const damages = [
  { name: "キャラクター1", value: 1200, color: "#e76f51" },
  { name: "キャラクター2", value: 900, color: "#2a9d8f" },
  { name: "キャラクター3", value: 700, color: "#e9c46a" },
  { name: "キャラクター4", value: 500, color: "#457b9d" },
];
//キャラクターはダメージ順に並べる必要あれば修正必要//
// メモのエリア→<template>エリア<!--　--><script>エリア// //1行のコメント<styleエリア>/* */ //
const totalDamage = computed(() => damages.reduce((sum, character) => sum + character.value, 0));
const maxDamage = computed(() => Math.max(...damages.map((character) => character.value)));
const pieStyle = computed(() => {
  let start = 0;
  const sections = damages.map((character) => {
    const end = start + (character.value / totalDamage.value) * 100;
    //${} は、「ここにJavaScriptの値を入れてください」//
    const section = `${character.color} ${start}% ${end}%`;
    //文字列に変数を埋め込むときは``で囲む//
    start = end;
    return section;
  });
  return {
    background: `conic-gradient(${sections.join(",")})`,
  };
});
const isOpen = ref(false);


const selectedCharacter = ref(characters[0]);
const selectedWeapon = ref(characters[0].weapons[0]);
const selectCharacter = (character) => {
  selectedCharacter.value = character;
  selectedWeapon.value = character.weapons[0] ?? "";
  isOpen.value = false;
};
const availableWeapons = computed(() => {
  return weapons.filter((weapon) =>
    selectedCharacter.value.weapons.includes(weapon.id)
  );
});
const selectedWeaponData = computed(() => {
  return weapons.find((weapon) => weapon.id === selectedWeapon.value);
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

  <section id="next-steps">
    <div id="docs">
      <div class="mb-1 grid grid-cols-4">
        <div class="flex-auto text-center bg-[#214753] border border-[#060d0f] py-2">
          <div class="character-selector">
            <button class="character-button" @click="isOpen = !isOpen">
              {{ selectedCharacter.icon }}
            </button>
            <div v-if="isOpen" class="character-menu">
              <div v-for="character in characters" :key="character.id" class="character-item" @click="selectCharacter(character)">
                <span class="icon">{{ character.icon }}</span>
                <span>{{ character.name }}</span>
              </div>
            </div>
          </div>
        </div>
        <div class="flex-auto text-center bg-[#214753] border border-[#060d0f] py-2">"tab2"</div>
        <div class="flex-auto text-center bg-[#214753] border border-[#060d0f] py-2">"tab3"</div>
        <div class="flex-auto text-center bg-[#214753] border border-[#060d0f] py-2">"tab4"</div>
      </div>

      <div class="mb-2 border border-[#333333] bg-gradient-to-r from-[#010102cc] to-[#222222cc] py-2">
        <div class="flex justify-between flex-wrap">
          <div class="flex basis-full md:basis-1/2 sm:basis-2/5 sm:block justify-evenly mb-2">
            <div class="sm:block">
              PTバフ
              <div class="flex gap-2 justify-center">
                <img :src="autoIcon" class="top-icon" width="40" height="40" />
                <img :src="autoIcon" class="top-icon" width="40" height="40" />
              </div>
            </div>
            <div class="flex justify-center gap-2">
              <div>Lv:90</div>
              <div>天賦Lv:10</div>
            </div>
            <div class="weapon-selector">
            <label for="weapon-select">武器：</label>
            <select id="weapon-select" v-model="selectedWeapon">
              <option v-for="weapon in availableWeapons" :key="weapon.id" :value="weapon.id">
                {{ weapon.name }}
              </option>
            </select>
          </div>
          <div class="selection-result">
            <p>キャラクター：{{ selectedCharacter.name }}</p>
            <p>武器：{{ selectedWeaponData?.name }}</p>
          </div>
          </div>

          <div class="basis-full md:basis-1/2 sm:basis-3/5 sm:block">
            <img :src="autoIcon" class="top-icon" width="40" height="40" />
            <calcDmg />
          </div>
        </div>
      </div>
    </div>

    <div class="damage-charts">
      <h2>キャラクター別ダメージ</h2>
      <p>合計ダメージ: {{ totalDamage }}</p>

      <div class="chart-layout">
        <div class="bar-chart" aria-label="棒グラフ">
          <div class="bar-row">
            <span>キャラクター</span>
            <span>グラフ</span>
            <span>ダメージ</span>
          </div>
          <div v-for="character in damages" :key="character.name" class="bar-row">
            <span>{{ character.name }}</span>
            <div class="bar-background">
              <div class="bar" :style="{ width: `${(character.value / maxDamage) * 100}%`, backgroundColor: character.color }"></div>
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
  </section>
</template>
