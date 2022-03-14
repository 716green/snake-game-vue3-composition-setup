<script setup>
import { onMounted, ref } from "vue";
const direction = ref("");
const playerXPos = ref(0);
const playerYPos = ref(0);
const gameSpeed = ref(250);

const listenForKey = ({ key }) => {
  if (["w", "a", "s", "d"].indexOf(key) !== -1) {
    const normalizedKey = key.toLowerCase();
    if (normalizedKey === "w") direction.value = "up";
    else if (normalizedKey === "a") direction.value = "left";
    else if (normalizedKey === "s") direction.value = "down";
    else if (normalizedKey === "d") direction.value = "right";
  }
};

const goUp = () => {
  playerYPos.value = playerYPos.value - 50;
  const player = document.getElementById("player");
  player.style.top = playerYPos.value + "px";
};
const goLeft = () => {
  playerXPos.value = playerXPos.value - 50;
  const player = document.getElementById("player");
  player.style.left = playerXPos.value + "px";
};
const goDown = () => {
  playerYPos.value = playerYPos.value + 50;
  const player = document.getElementById("player");
  player.style.top = playerYPos.value + "px";
};
const goRight = () => {
  playerXPos.value = playerXPos.value + 50;
  const player = document.getElementById("player");
  player.style.left = playerXPos.value + "px";
};

const nextMove = () => {
  if (direction.value === "up") goUp();
  if (direction.value === "down") goDown();
  if (direction.value === "left") goLeft();
  if (direction.value === "right") goRight();
};

const startTimer = () => {
  setInterval(() => {
    nextMove();
  }, gameSpeed.value);
};

onMounted(() => {
  document.addEventListener("keypress", listenForKey);
  startTimer();
});
</script>

<template>
  <div id="player">
    x: {{ playerXPos }}<br />
    y: {{ playerYPos }}
  </div>
</template>

<style lang="css" scoped>
#player {
  width: 50px;
  height: 50px;
  position: relative;
  background-color: blueviolet;
  left: var(playerXPos);
  top: var(playerYPos);
  border: 4px gray dotted;
  box-sizing: border-box;
  opacity: 100;
  font-size: 0.7rem;
  padding: 2px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: white;
}
</style>
