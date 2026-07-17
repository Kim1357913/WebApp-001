<script setup>
import { ref,reactive,computed } from 'vue'
import charaNad09Img from '../assets/Char-Nad-09/Char.png'
import autoIcon from '../assets/Char-Nad-09/Bow_Geo.webp'
import skill1Icon from '../assets/Char-Nad-09/Talent_Countermeasure-_Lumi21.webp'
import skill2Icon from '../assets/Char-Nad-09/Talent_Memo-_Survival_Guide_in_Extreme_Conditions.webp'
import talent1Icon from '../assets/Char-Nad-09/Talent_Field_Observation_Notes.webp'
import Charactor from './Char-Nad-09.vue'
import demoGrid from './Grid.vue'
import calcDmg from './CalcDmg.vue/index.js'
import 
const isHovered  = ref(false)
const mouseOverAction = () => {
  isHovered.value = true
}
const mouseOutAction = () => {
  isHovered.value = false
}
const isOpen = ref(false);

  const searchQuery = ref('')
const gridColumns = ['name','equipment', 'power']
const gridData = [
  { name: 'Chuck Norris', equipment: 'Infinity', power: Infinity },
  { name: 'Bruce Lee', equipment: '9000', power: 9000 },
  { name: 'Jackie Chan', equipment: '7000', power: 7000 },
  { name: 'Jet Li', equipment: '8000', power: 8000 }
]
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
    
  </section>

  <div class="ticks"></div>

  <section id="next-steps">   
    <div id="docs">
     <div class="area">
        <input type="radio" name="tab_name" id="tab1" checked>
        <label class="tab_class" for="tab1">タブ1</label>
        <div class="content_class">
          <p>タブ1のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab2" >
        <label class="tab_class" for="tab2">タブ2</label>
        <div class="content_class">
          <p>タブ2のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab3" >
        <label class="tab_class" for="tab3">タブ3</label>
        <div class="content_class">
          <p>タブ3のコンテンツを表示します</p>
        </div>
        <input type="radio" name="tab_name" id="tab4" >
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
     <p><CalcDmg /></p>
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

