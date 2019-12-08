<template>
  <div class="VueToNuxtLogo">
    <div class="Triangle Triangle--two" />
    <div class="Triangle Triangle--one" />
    <div class="Triangle Triangle--three" />
    <div class="Triangle Triangle--four" />
  </div>
</template>

<style>
.VueToNuxtLogo {
  display: inline-block;
  animation: turn 2s linear forwards 1s;
  transform: rotateX(180deg);
  position: relative;
  overflow: hidden;
  height: 45px;
  width: 64px;
}

.Triangle {
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 0;
}

.Triangle--one {
  border-left: 26.25px solid transparent;
  border-right: 26.25px solid transparent;
  border-bottom: 45px solid #41b883;
}

.Triangle--two {
  top: 7.5px;
  left: 8.75px;
  animation: goright 0.5s linear forwards 3.5s;
  border-left: 21.875px solid transparent;
  border-right: 21.875px solid transparent;
  border-bottom: 37.5px solid #3b8070;
}

.Triangle--three {
  top: 15px;
  left: 8.75px;
  animation: goright 0.5s linear forwards 3.5s;
  border-left: 17.5px solid transparent;
  border-right: 17.5px solid transparent;
  border-bottom: 30px solid #35495e;
}

.Triangle--four {
  top: 30px;
  left: 17.5px;
  animation: godown 0.5s linear forwards 3s;
  border-left: 8.75px solid transparent;
  border-right: 8.75px solid transparent;
  border-bottom: 15px solid #fff;
}

@keyframes turn {
  100% {
    transform: rotateX(0deg);
  }
}

@keyframes godown {
  100% {
    top: 45px;
  }
}

@keyframes goright {
  100% {
    left: 19px;
  }
}
</style>
