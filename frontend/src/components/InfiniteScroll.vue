<script setup>

</script>

<template>
  <div class="scroll imgBox" style="--time:25s">
    <div>
      <slot></slot>
    </div>
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<!--suppress CssInvalidPropertyValue -->
<style scoped>
/*  Scroll Effect */
.scroll {
  position: relative;
  display: flex;
  width: 100%;
  overflow: hidden;
  z-index: -5;
  mask-image: linear-gradient(90deg, transparent, #fff 20%, #fff 80%, transparent);
}

.scroll div {
  white-space: nowrap;
  animation: scroll var(--time) linear infinite;
  animation-delay: calc(var(--time)*-1);

}

.scroll div:nth-child(2) {
  animation: scroll2 var(--time) linear infinite;
  animation-delay: calc(var(--time)/-2);
}

@keyframes scroll {
  0% {
    transform: translateX(100%);
  }

  100% {
    transform: translateX(-100%);
  }
}

@keyframes scroll2 {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(-200%);
  }
}

.scroll div span {
  display: inline-flex;
  margin: 10px;
  letter-spacing: 0.2em;
  background: #333;
  color: #fff;
  padding: 5px 10px;
  border-radius: 5px;
  transition: 0.5s;
}

.scroll div span:hover {
  background: #3fd2f9;
  cursor: pointer;
}

.imgBox div {
  display: flex;
  align-items: center;
  justify-content: center;
}

.imgBox :deep(img) {
  width: 500px;
  height: 500px;
  object-fit: cover;

  /* Phone */
  @media (max-width: 850px) {
    width: 250px;
    height: 250px;
  }
}
</style>