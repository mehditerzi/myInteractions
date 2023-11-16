<script setup lang="js">
import {ref,onMounted} from "vue";

let isDragging = false;
let startx = null;
let activex = null;
const revealcontainer = ref(null);
const slider = ref(null);
function startDrag(event) {
  isDragging= true;
  startx = event.clientX;
}
function resizeImg(event) {
  if (isDragging){
    var activex = event.clientX;
    var newWidth = activex-startx;
    revealcontainer.value.style.width = activex + 'px';
    slider.value.style.left = activex + 'px';
  }
}
function endDrag() {
  isDragging= false;
}
</script>

<template>
<div class="container" @mousemove="resizeImg" @mouseleave="endDrag" @mouseup="endDrag">>
  <img src="/imageblurry.png" class="baseimg" alt="originalimage">
  <div class="revealcontainer" style="width: 0px;" ref="revealcontainer">
    <img src="/image.png" alt="newimg" class="revealimg">
  </div>
  <div class="revealslider" style="left: 0px;" ref="slider" @mousedown="startDrag" @mouseup="endDrag"></div>
</div>
</template>

<style scoped>
img{
  user-select: none;
}
.container{
  position: relative;
  width: 40em;
  height: 20em;
  background: gray;
}
.baseimg{
  position: absolute;
  top: 0;
  left: 0;
  width: 40em;
  height: 20em;
  object-fit: cover;
}
.revealcontainer{
  position: absolute;
  top: 0;
  left: 0;
  overflow: hidden;
  height: 100%;
}
.revealimg{
  height: 20em;
  width: 40em;
  object-fit: cover;
}
.revealslider{
  width: 1em;
  height: 100%;
  background: black;
  cursor: grab;
  position: absolute;
  top: 0;
  left: 0;
}
</style>