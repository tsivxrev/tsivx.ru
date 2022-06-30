<script>
export default {
    data() {
      return {
        title: "Арсений Циварев",
        subtitle: "Тюмень, Россия",
        avatar_url: "/avatar.jpg",
        socials: []
      }
    },
    computed: {
      socialsEmpty() {
        return this.socials.length == 0
      }
    },
    async mounted() {
      const response = await fetch('https://stage-api.tsivx.workers.dev/landing/info');
      const info = await response.json();

      Object.assign(this.$data, info)
    }
  }
</script>

<template>
  <section class="main flex items-center flex-col justify-center bg-neutral-900 p-8 w-screen h-screen">
    <div class="card flex flex-col gap-4 justify-center bg-neutral-800 p-8 rounded-lg max-w-lg">
      <div class="header flex items-center gap-4 flex-row">
          <div class="avatar">
            <img class="rounded-full w-24" :src="avatar_url">
          </div>
          <div class="info">
            <div class="title font-semibold text-2xl text-white">{{title}}<!-- <span class="text-neutral-500 font-normal text-lg">16 лет</span> --></div>
            <div class="subtitle font-normal text-neutral-500 text-lg">{{subtitle}}</div>
          </div>
      </div>
      <div class="socials flex flex-wrap gap-2">
        <div v-if="socialsEmpty" class="text-center text-white w-full animate-pulse">Загрузка...</div>
        <a v-for="social in socials" :href="social.link" class="social hover:bg-indigo-600 text-center rounded-full px-4 py-2 bg-indigo-700 text-white font-medium">{{social.title}}</a>
      </div>
    </div>
  </section>
</template>