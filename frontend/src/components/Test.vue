<script setup>
import { ref,reactive,computed } from 'vue'
import charaNad09Img from '../assets/chara-img/nad09.png'
import autoIcon from '../assets/chara-img/Bow_Geo.webp'
import skill1Icon from '../assets/chara-img/Talent_Countermeasure-_Lumi21.webp'
import skill2Icon from '../assets/chara-img/Talent_Memo-_Survival_Guide_in_Extreme_Conditions.webp'
import talent1Icon from '../assets/chara-img/Talent_Field_Observation_Notes.webp'
import Charactor from './charactor.vue'
const isHovered  = ref(false)

const mouseOverAction = () => {
  isHovered.value = true
}

const mouseOutAction = () => {
  isHovered.value = false
}

const isOpen = ref(false)
const mainStatusRef = ref(1000) // 仮のメインステータス値
const 天賦倍率 = 172.8 * 2 * 0.01  // 仮の天賦倍率
const 特殊乗算 = 1.0 // 仮の特殊乗算
const 実数ダメージ加算 = 0 // 仮の実数ダメージ加算
const ダメージバフ補正 = 1.0 // 仮のダメージバフ補正
const 会心補正 = 1.0 // 仮の会心補正
const skillDMG = computed(() => {
  return  ((mainStatusRef.value * 天賦倍率 * 特殊乗算 + 実数ダメージ加算) * ダメージバフ補正 * 会心補正)
})  
</script>

<template>
  <section id="top-steps">
    <div class="hero">
      <img :src="charaNad09Img" class="base"  width="718" height="440"alt="" />
    </div>
    <ul>
      <a @mouseover="mouseOverAction" @mouseout="mouseOutAction">
        <li>
            <img :src="autoIcon"class="top-icon" role="presentation" aria-hidden="true" /> 
            <div class="skillExplain1" v-if="isHovered"><Charactor /></div>
        </li>
      </a>
      <a>
        <li>
            <img :src="skill1Icon"class="top-icon" role="presentation" aria-hidden="true" />  
        </li>
     </a>
     <a>
      <li>
            <img :src="skill2Icon"class="top-icon" role="presentation" aria-hidden="true" />  
        </li>
     </a>
        
    </ul>
    <div>
      <h2>元素スキル</h2>
      <p> ルミのやっふー作戦
       <div>スキル選択: {{ スキル選択 }}</div>

     <select v-model="スキル選択">
      <option disabled value="">Please select one</option>
      <option>スキル1</option>
      <option>スキル2</option>
      <option>スキル3</option>
     </select>
      <code>スキルダメージ</code>ポコポコハンマー172.8%×2 ({{skillDMG}})</p>
    </div>
    
  </section>

  <div class="ticks"></div>

  <section id="next-steps">
    <div id="docs">
      <svg class="icon" role="presentation" aria-hidden="true">
        <use href="/icons.svg#documentation-icon"></use>
      </svg>
      <h2>Documentation</h2>
      <p>Your questions, answered</p>
      <ul>
        <li>
          <a href="https://vite.dev/" target="_blank">
            <img class="logo" :src="viteLogo" alt="" />
            Explore Vite
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

