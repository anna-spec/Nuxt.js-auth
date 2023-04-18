<template>
  <div id="project-bar" class="c-projects-bar">
      <nuxt-link tag="div" to="/">
        <img
        width="30"
        height="30"
        src="https://api.quwi.com/images/logo_150.png"
      />
      </nuxt-link>
  </div>
</template>
<script></script>

<style lang="scss">
.c-projects-bar {
  background: #fafafa;
  border-top-color: transparent;
  width: 70px;
  height: 100%;
  z-index: 1002;
  position: fixed;
  left: 0;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.25);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  div{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
    cursor: pointer;
  }
}
</style>