<template>
    <div class="content">
      <div class="preview">
        <div class="preview-content">
          <div class="top-row">
            <img :src="selectedRobot.head.imageUrl" alt="robot-part" />
          </div>
          <div class="middle-row">
            <img :src="selectedRobot.leftArm.imageUrl" class="rotate-left" alt="robot-part" />
            <img :src="selectedRobot.torso.imageUrl" alt="robot-part" />
            <img :src="selectedRobot.rightArm.imageUrl" class="rotate-right" alt="robot-part" />
          </div>
          <div class="bottom-row">
            <img :src="selectedRobot.bottom.imageUrl" alt="robot-part" />
          </div>
        </div>
        <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
  </div>
  <div class="top-row">
     <div class="robot-name">
      {{selectedRobot.head.title}}
      <span class="sale" v-if="selectedRobot.head.onSale">Sale!</span>
    </div>
    <PartSelector :parts="availableParts.heads" position="top"
    @partSelected="part => selectedRobot.head=part"/>
  </div>
  <div class="middle-row">
    <PartSelector :parts="availableParts.arms" position="left"
    @partSelected="part => selectedRobot.leftArm=part" />
    <PartSelector :parts="availableParts.torsos" position="center"
    @partSelected="part => selectedRobot.torso=part" />
    <PartSelector :parts="availableParts.arms" position="right"
    @partSelected="part => selectedRobot.rightArm=part" />
  </div>
  <div class="bottom-row">
    <PartSelector :parts="availableParts.bases" position="bottom"
    @partSelected="part => selectedRobot.bottom=part" />
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
      <tr v-for="(robot, index) in cartStore.cart" :key="index">
        <td>{{ robot.head.title }}</td>
        <td class="cost">{{ toCurrency(robot.cost) }}</td>
        <!--<td class="cost"><pre>{{ robot }}</pre></td>-->
      </tr>
    </tbody>
  </table>
</div>
</template>
<script setup>
import { ref } from 'vue';
import toCurrency from '../shared/formatters';
import PartSelector from './PartSelector.vue';
import parts from '../data/parts';
import { useCartStore } from '../stores/cartStore';

const availableParts = parts;
const cartStore = useCartStore();
const selectedRobot = ref({
  head: {},
  leftArm: {},
  rightArm: {},
  bottom: {},
  torso: {},
});

const addToCart = () => {
  const robot = selectedRobot.value;
  const cost = robot.head.cost +
    robot.leftArm.cost +
    robot.torso.cost +
    robot.rightArm.cost +
    robot.bottom.cost;
  cartStore.cart.push({ ...robot, cost });
  console.log(cartStore.cart.length);
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

.preview {
  position: absolute;
  top: -20px;
  right: 0;
  width: 310px;
  height: 310px;
  padding: 5px;
}

.preview-content {
  border: 1px solid #999;
}

.preview img {
  width: 70px;
  height: 70px;
}

.rotate-right {
  transform: rotate(90deg);
}

.rotate-left {
  transform: rotate(-90deg);
}

.add-to-cart {
  position: absolute;
  width: 310px;
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
