<template>
    <div class="content">
      <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
  <div class="top-row">
     <div class="robot-name">
      {{selectedRobot.head.title}}
      <span class="sale" v-if="selectedRobot.head.onSale">Sale!</span>
    </div>
    <PartSelector :parts="availableParts.heads" position="top" />
  </div>
  <div class="middle-row">
    <PartSelector :parts="availableParts.arms" position="left" />
    <PartSelector :parts="availableParts.torsos" position="center" />
    <PartSelector :parts="availableParts.arms" position="right" />
  </div>
  <div class="bottom-row">
    <PartSelector :parts="availableParts.bases" position="bottom" />
  </div>
  <h1>Cart</h1>
  <table>
    <thead>
      <tr>
        <th>Robot</th>
        <th class="cost">Cost</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(robot, index) in cart" :key="index">
        <td>{{ robot.head.title }}</td>
        <td class="cost">{{ toCurrency(robot.cost) }}</td>
      </tr>
    </tbody>
  </table>
</div>
</template>
<script setup>
import { ref } from 'vue';
import toCurrency from '@/shared/formatters';
import PartSelector from './PartSelector.vue';
import parts from '../data/parts';

const availableParts = parts;
const cart = ref([]);
const selectedRobot = ref({
  head: {},
  leftArm: {},
  rightArm: {},
  base: {},
  torso: {},
});

const addToCart = () => {
  const robot = selectedRobot.value;
  const cost = robot.head.cost +
    robot.leftArm.cost +
    robot.torso.cost +
    robot.rightArm.cost +
    robot.base.cost;
  cart.value.push({ ...robot, cost });
  console.log(cart.value.length);
};

</script>
<style>
.part {
  position: relative;
  width: 200px;
  height: 200px;
  border: 3px solid #aaa;
}

.part img {
  width: 200px;
}

.top-row {
  display: flex;
  justify-content: space-around;
}

.middle-row {
  display: flex;
  justify-content: center;
}

.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.top {
  border-bottom: none;
}

.left {
  border-right: none;
}

.right {
  border-left: none;
}

.left img {
  transform: rotate(-90deg);
}

.right img {
  transform: rotate(90deg);
}

.bottom {
  border-top: none;
}

.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 206px;
}

.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 206px;
}

.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}

.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  right: -3px;
}

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}

.sale {
  color: red;
}

.content {
  position: relative;
}

.add-to-cart {
  position: absolute;
  right: 30px;
  width: 220px;
  padding: 3px;
  font-size: 16px;
}

td, th {
  text-align: left;
  padding: 5px;
  padding-right: 20px;
}

.cost {
  text-align: right;
}
</style>
