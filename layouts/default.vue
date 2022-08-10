<template>
  <div class="content" :class="{ showcredits: $store.state.credits }">
    <header class="header">
      <div class="col col-one">
        Cipher
      </div>

      <div class="col col-two">
        <a href="#download">Download</a>
      </div>

      <div class="col col-three">
        <a :href="twitterLink" @click="onShare">Share</a>
      </div>

      <div class="col col-four">
        <a href="#credits">Credits</a>
      </div>
    </header>

    <div class="credits" :aria-hidden="$store.state.credits ? 'true' : 'false'">
      <div class="credits-left">
        <p>
          DjqifsVF.ttf / Cipher is a project made by
          <a href="https://jthaw.me" target="_blank">Jonny Thaw</a>. It explores
          the use of a simple cipher trick to hide information out in plain
          site. All the robots can read this, but silly old humans can't.
        </p>
        <p>
          All credit to the fantastic work of
          <a href="https://gent.media/" target="_blank">Mikhail Sharanda</a>,
          who not only made an incredible font, but generously gave it a license
          to allow me to do a project like this.
        </p>
        <p>
          Poster mockup can be
          <a
            href="https://www.freepik.com/free-psd/colorful-gradient-poster-mockup-psd-glued-wall_17860998.htm#query=poster%20mockup&position=16&from_view=keyword"
            target="_blank"
            class="less"
            >found here</a
          >
        </p>

        <p><a href="#">Close</a></p>
      </div>

      <div class="credits-right">
        <p>
          <a href="https://manropefont.com" target="_blank">FONT CREDIT</a>
          <a href="https://manropefont.com" target="_blank">FONT CREDIT</a>
          <a href="https://manropefont.com" target="_blank">FONT CREDIT</a>
          <a href="https://manropefont.com" target="_blank">FONT CREDIT</a>
          <a href="https://manropefont.com" target="_blank">FONT CREDIT</a>
        </p>
      </div>
    </div>

    <nuxt />
  </div>
</template>

<script>
import smoothscroll from "smoothscroll-polyfill";
import { listenCb, registerBootlegVH, tickUpdate } from "~/assets/js/utils";
import { BreakPointSet } from "~/assets/js/mixins/breakpoints";

const TITLE = ["DjqifsVF.ttf", "IS", "WHAT", "IT", "IS", "~"];

export default {
  mixins: [BreakPointSet],
  data() {
    return {
      icon: 1
    };
  },
  computed: {
    currentRoute() {
      return this.$route.path;
    },
    twitterLink() {
      return `https://cipher.jthaw.club`;
    }
  },
  mounted: function() {
    smoothscroll.polyfill();

    registerBootlegVH();
    this.interval = setInterval(this.changeFavicon.bind(this), 500);

    // prevent the add to home screen banner
    this.unlisten = [
      listenCb(window, "beforeinstallprompt", e => {
        e.preventDefault();
      }),

      // listenCb(window, "hashchange", this.onHashChange.bind(this)),
      listenCb(window, "popstate", this.onHashChange.bind(this)),
      () => clearInterval(this.interval),
      listenCb(document, "mousewheel", tickUpdate(this.onScroll.bind(this)))
    ];

    this.onHashChange();
  },
  beforeDestroy() {
    this.unlisten && this.unlisten.forEach(cb => cb());
  },
  methods: {
    onPreloaderDisappear() {
      this.$store.commit("setPreloaderActive", false);
    },
    changeFavicon() {
      this.icon = (this.icon + 1) % 6;
      document.querySelector("link[rel~='icon']").href = `/icon${this.icon +
        1}.png`;
      document.querySelector("title").innerText = TITLE[this.icon];
    },
    onHashChange() {
      const url = window.location.href.split(window.location.origin).join("");

      const isCredits = url.includes("credits");

      this.$store.commit("setCredits", isCredits);
    },
    onShare(e) {
      if ("share" in navigator) {
        e.preventDefault();

        const data = {
          url: `https://cipher.jthaw.club`,
          text: "DjqifsVF.ttf is what it is"
        };

        navigator.share(data);
      }
    },
    onScroll(e) {
      if (e.deltaY > 100) {
        window.location.hash = "#";
      }
    }
  }
};
</script>
<style lang="scss">
@import "~assets/scss/parts/fonts";

:root {
  --color-white: #e9e5d9;
  --color-black: #000;

  --color-red: #f12323;
  --color-blue: #2376f1;

  --color-text: var(--color-white);
  --color-bg: var(--color-black);

  --font-size-x-small: 10px;
  --font-size-small: 12px;
  --font-size-normal: 16px;
  --font-size-medium: 21px;
  --font-size-large: 24px;
  --font-size-x-large: 36px;
  --font-size-xx-large: 46px;
  --font-size-xxx-large: 56px;

  --font-family-body: "DjqifsVF", sans-serif;
  --font-family-headline: sans-serif;

  --header-height: 60px;

  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-bold: 700;
  --font-weight-extra-bold: 900;

  @for $i from 1 through 20 {
    --size-unit-#{$i}: #{$i * 5px};
  }
}

// ::-webkit-scrollbar {
//   width: 0px; /* remove scrollbar space */
//   background: transparent; /* optional: just make scrollbar invisible */
// }

*,
*:before,
*:after {
  box-sizing: border-box;
}

html {
  font-family: var(--font-family-body);
  font-size: var(--font-size-normal);
  color: var(--color-text);

  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;

  background-color: var(--color-bg);

  line-height: 1.25;

  scroll-behavior: smooth;
}

input,
button {
  font-family: inherit;
  font-weight: inherit;
}

html,
body {
  width: 100%;
  min-height: 100%;
}

.visually-hidden {
  clip: rect(0 0 0 0);
  clip-path: inset(50%);
  height: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}

.fade {
  opacity: 1;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.fade-fast {
  opacity: 1;
}

.fade-fast-enter-active,
.fade-fast-leave-active {
  transition: opacity 0.5s;
}
.fade-fast-enter, .fade-fast-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

img {
  max-width: 100%;
}

.header {
  position: sticky;

  top: 0;

  display: grid;

  z-index: 10;

  grid-template-columns: repeat(12, 1fr);
  gap: 20px;

  background-color: var(--color-bg);

  padding: 20px;

  font-weight: bold;
  text-transform: uppercase;

  a {
    color: inherit;

    text-decoration: none;

    &:hover,
    &:focus-visible {
      color: var(--color-red);
    }
  }

  .col {
    @include tablet {
      &-one {
        grid-column: 1 / span 3;
      }

      &-two {
        grid-column: 4 / span 2;
      }

      &-three {
        grid-column: 7 / span 2;
      }

      &-four {
        grid-column: 11 / span 2;

        text-align: right;
      }
    }
  }

  .showcredits & {
    transform: translate3d(
      0,
      calc((var(--vh) * 100) - var(--header-height)),
      0
    );
  }
}

.credits {
  padding: 20px;

  background-color: var(--color-red);

  transform: translate3d(0, -100%, 0);

  z-index: 8;

  width: 100%;
  height: calc((var(--vh) * 100) - var(--header-height));

  position: fixed;

  top: 0;
  left: 0;

  display: grid;

  gap: 10px;

  &-left {
  }

  p {
    a {
      color: var(--color-bg);

      text-decoration: none;

      &:hover,
      &:focus-visible {
        color: var(--color-blue);
      }

      &.less {
        color: inherit;
      }
    }
  }

  &-right {
    align-self: flex-end;
    a {
      display: none;

      font-size: 36px;

      &:first-child {
        display: block;
      }
    }
  }

  .showcredits & {
    transform: translate3d(0, 0, 0);
  }

  @include tablet {
    grid-template-columns: repeat(12, 1fr);

    &-left {
      grid-column: 1 / span 5;
    }

    &-right {
      align-self: flex-start;
      text-align: right;
      grid-column: 9 / span 4;
      a {
        display: block;
      }
    }
  }
}

.header,
.credits {
  transition: {
    duration: 0.5s;
    property: transform;
  }
}
</style>
