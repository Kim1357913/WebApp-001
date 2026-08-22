<script setup>
import { ref,reactive,computed } from 'vue'
const stats = reactive([
  { label: '防御力%', value: 200 },
  { label: 'ダメージバフ', value: 100 },
  { label: '会心ダメージ', value: 100 },
  { label: '会心率', value: 50 },
  { label: 'E', value: 100 },
  { label: 'F', value: 100 }
])
const 基礎防御力 = 1000; // 仮のメインステータス値
const 防御力補正 = computed(() => {
  return stats[0].value * 0.01 }); // 防御力補正はスライダーの値を百分率に変換
const 天賦倍率 = 172.8 * 2 * 0.01; // 仮の天賦倍率
const 特殊乗算 = 1.0 ;// 仮の特殊乗算
const 実数ダメージ加算 = 0 ;// 仮の実数ダメージ加算
const ダメージバフ補正 = computed(() => {
  return 1 + (stats[1].value * 0.01) });// ダメージバフ補正はスライダーの値を百分率に変換
const 会心補正 = computed(() => {
  const critrate = Math.min(stats[3].value, 100) * 0.01 // 会心率は最大100%まで
  const critdamage = stats[2].value * 0.01 // 会心ダメージはスライダーの値を百分率に変換
  return 1 + (critrate * critdamage) });// 会心補正は会心率と会心ダメージの組み合わせ
const skillDMG = computed(() => {
  return  (基礎防御力 + (基礎防御力 * 防御力補正.value))});// 最終的なダメージ計算 
  //月結晶反応ダメージ扱い
  // 1.6*防御力*倍率*(1+月結晶反応ダメージアップ%)*(1+元素熟知による月結晶ボーナス+月結晶バフ%)*会心補正
  //月結晶反応
  // 反応キャラレベル補正*0.96*元素熟知*会心*別枠乗算
</script>

<template>
    <div v-for="stat in stats">
        <label>{{stat.label}}</label>
        <input type="range" v-model="stat.value" min="0" max="100">
        <span>{{stat.value}}</span>
      </div>
  <!--<div>スキル選択: {{ スキル選択 }}</div>
         <select v-model="スキル選択">
        <option disabled value="">Please select one</option>
        <option>スキル1</option>
        <option>スキル2</option>
        <option>スキル3</option>
         </select>
         <code>スキルダメージ</code>ポコポコハンマー172.8%×2 ({{skillDMG}})({{基礎防御力 * 防御力補正}})
-->
</template>