<template>
  <div class="card">
    <img
      class="bg"
      :src="data.image"
      :style="`object-position: ${data.focus[0]}% ${data.focus[1]}%`"
    />
    <img
      class="image"
      :src="data.image"
      :style="`object-position: ${data.focus[0]}% ${data.focus[1]}%`"
    />
    <div class="banner">
      <div class="logo">
        <svg
          width="49"
          height="65"
          viewBox="0 0 49 65"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M13.248 26.64C10.688 26.64 8.4 26.064 6.384 24.912C4.4 23.728 2.832 22.144 1.68 20.16C0.56 18.144 0 15.872 0 13.344C0 10.752 0.56 8.448 1.68 6.432C2.8 4.416 4.336 2.848 6.288 1.728C8.24 0.575999 10.48 0 13.008 0C14.896 0 16.624 0.368 18.192 1.104C19.76 1.808 21.168 2.88 22.416 4.32C22.864 4.832 23.024 5.36 22.896 5.904C22.768 6.448 22.416 6.928 21.84 7.344C21.392 7.664 20.896 7.776 20.352 7.68C19.808 7.552 19.312 7.264 18.864 6.816C17.296 5.152 15.344 4.32 13.008 4.32C11.376 4.32 9.936 4.704 8.688 5.472C7.44 6.208 6.464 7.248 5.76 8.592C5.056 9.936 4.704 11.52 4.704 13.344C4.704 15.072 5.056 16.608 5.76 17.952C6.496 19.296 7.504 20.368 8.784 21.168C10.064 21.936 11.552 22.32 13.248 22.32C14.368 22.32 15.344 22.192 16.176 21.936C17.04 21.648 17.824 21.216 18.528 20.64C19.04 20.224 19.568 20 20.112 19.968C20.656 19.904 21.136 20.048 21.552 20.4C22.096 20.848 22.4 21.36 22.464 21.936C22.528 22.48 22.336 22.976 21.888 23.424C19.584 25.568 16.704 26.64 13.248 26.64Z"
            fill="white"
          />
          <path
            d="M13.224 64.128C10.728 64.128 8.48799 63.552 6.50399 62.4C4.51999 61.216 2.95199 59.616 1.79999 57.6C0.647987 55.584 0.0559869 53.312 0.0239868 50.784V28.896C0.0239868 28.16 0.247987 27.568 0.695987 27.12C1.17599 26.672 1.76799 26.448 2.47199 26.448C3.20799 26.448 3.79999 26.672 4.24799 27.12C4.69599 27.568 4.91999 28.16 4.91999 28.896V41.856C6.03999 40.512 7.38399 39.456 8.95199 38.688C10.552 37.888 12.296 37.488 14.184 37.488C16.52 37.488 18.616 38.08 20.472 39.264C22.328 40.416 23.784 42 24.84 44.016C25.928 46 26.472 48.256 26.472 50.784C26.472 53.312 25.88 55.584 24.696 57.6C23.544 59.616 21.976 61.216 19.992 62.4C18.008 63.552 15.752 64.128 13.224 64.128ZM13.224 59.808C14.856 59.808 16.312 59.424 17.592 58.656C18.872 57.856 19.88 56.768 20.616 55.392C21.384 54.016 21.768 52.48 21.768 50.784C21.768 49.056 21.384 47.52 20.616 46.176C19.88 44.832 18.872 43.776 17.592 43.008C16.312 42.208 14.856 41.808 13.224 41.808C11.624 41.808 10.168 42.208 8.85599 43.008C7.57599 43.776 6.56799 44.832 5.83199 46.176C5.09599 47.52 4.72799 49.056 4.72799 50.784C4.72799 52.48 5.09599 54.016 5.83199 55.392C6.56799 56.768 7.57599 57.856 8.85599 58.656C10.168 59.424 11.624 59.808 13.224 59.808Z"
            fill="white"
          />
          <path
            d="M45.008 25.968L27.296 15.36C26.432 14.816 26 14.08 26 13.152C26 12.32 26.432 11.6 27.296 10.992L45.008 0.336C45.872 -0.112 46.704 -0.112 47.504 0.336C48.304 0.751998 48.704 1.424 48.704 2.352C48.704 3.312 48.304 4.032 47.504 4.512L31.328 14.112V12.048L47.504 21.744C48.304 22.256 48.704 22.96 48.704 23.856C48.704 24.496 48.496 25.04 48.08 25.488C47.696 25.904 47.216 26.176 46.64 26.304C46.064 26.4 45.52 26.288 45.008 25.968Z"
            fill="white"
          />
        </svg>
      </div>
      <div class="info">
        Creative Code {{ data.format }} #{{ data.edition }}<br />
        {{
          data.when.toLocaleDateString("en-GB", {
            hour: "2-digit",
            month: "long",
            day: "numeric",
            minute: "2-digit",
          })
        }}<br />
        At {{ data.where }}
      </div>
      <div class="flap">
        <svg
          width="31"
          height="128"
          viewBox="0 0 31 128"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path d="M0 128V0H31V93L9 128H0Z" style="fill: var(--fg-1)" />
          <path d="M0 101L31 93L9 128L0 101Z" style="fill: var(--fg-2)" />
        </svg>
      </div>
    </div>
    <div class="author">{{ data.author ?? "Unknown Author" }}</div>
    <div class="site">creativecode.berlin</div>
  </div>
</template>

<script setup>
defineProps(["data"]);
</script>

<style scoped>
.card {
  background: var(--fg-1);
  zoom: 0.5;
  position: relative;
  color: white;
  font-size: 18px;
  line-height: 30px;
  overflow: hidden;
}
.banner {
  background: var(--fg-1);
  position: absolute;
  top: 43px;
  left: 0;
  height: 128px;
  display: flex;
  padding: 20px;
  padding-right: 40px;
  box-sizing: border-box;
}
.logo {
  margin: 20px;
}
.info,
.logo {
  align-self: center;
}
.flap svg {
  position: absolute;
  left: 100%;
  top: 0;
  height: 128px;
  width: 31px;
}
img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
}
.author {
  position: absolute;
  right: 20px;
  bottom: 20px;
  text-align: right;
  line-height: 18px;
}
.author:before {
  content: "art by";
  display: block;
  font-size: 14px;
}
.site {
  position: absolute;
  left: 20px;
  bottom: 20px;
  line-height: 18px;
}
.bg {
  filter: blur(10px);
  transform: scale(1.25);
}
</style>
