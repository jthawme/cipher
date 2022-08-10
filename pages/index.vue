<template>
  <div class="content">
    <div class="image" />

    <div id="download" />

    <div class="download">
      <div class="big">
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
        <span>DjqifsVF.ttf IS WHAT IT IS</span>
      </div>

      <div class="bottom">
        <a href="https://jthaw.me">jthaw.me</a>
        <a href="https://www.manropefont.com/">Download the actual font</a>
      </div>

      <a href="/DjqifsVF.ttf" download="DjqifsVF.ttf" class="downloadbtn">
        <span>Download</span>
        <span class="small">v1.0 variable font</span>
      </a>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.content {
}

.image {
  position: relative;

  z-index: 5;

  background-image: url("~/assets/img/HEADER.jpg");
  background-size: 100% auto;
  background-position: center;

  width: 100%;
  height: calc((var(--vh) * 100) - var(--header-height));

  @include tablet {
    background-size: cover;
  }
}

#download {
  height: vh(60);

  pointer-events: none;
}

.download {
  position: fixed;

  bottom: 0;

  width: 100%;
  height: vh(60);
  background-color: var(--color-blue);

  .big {
    position: absolute;

    top: 50%;
    left: 50%;

    width: 100%;

    transform: translate3d(-50%, -50%, 0);

    font-size: 6vw;

    text-align: center;

    line-height: 1;
    text-transform: uppercase;

    span {
      display: block;
    }
  }
}

.bottom {
  position: absolute;

  bottom: 0;
  left: 0;

  width: 100%;

  padding: 20px;

  display: flex;

  justify-content: space-between;

  font-size: 12px;

  a {
    color: var(--color-text);

    text-decoration: none;

    &:hover,
    &:focus-visible {
      color: var(--color-red);
    }
  }
}

.downloadbtn {
  position: absolute;

  top: 50%;
  left: 50%;

  transform: translate3d(-50%, -50%, 0);

  padding: 10px 30px;

  border: 3px solid var(--color-blue);
  background-color: var(--color-text);
  color: var(--color-blue);

  text-align: center;

  font-weight: bold;

  font-size: 3vw;

  display: flex;

  flex-direction: column;

  text-decoration: none;

  span {
    text-transform: uppercase;
  }

  .small {
    text-transform: none;
    font-weight: regular;

    font-size: 12px;
  }

  &:hover,
  &:focus-visible {
    color: var(--color-text);
    background-color: var(--color-blue);
  }
}
</style>
