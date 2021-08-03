<template>
  <div class="app">
    <section class="app-home">
      <h2 class="app-home__title">WELCOME</h2>
      <v-icon class="app-home__icon" color="white" @click="goToAboutMe">mdi-arrow-down</v-icon>
    </section>

    <section ref="about" class="app-about">
      <h3 class="app-about__title">ABOUT ME</h3>
      <div class="app-about__photo"></div>
      <div class="app-about__text app-about__text-container">
        <p class="app-about__text app-about__text--left">{{ aboutMe.left }}</p>
        <p class="app-about__text app-about__text--right">{{ aboutMe.right }}</p>
      </div>
    </section>

    <section class="app-tech-stack">
      <h3 class="app-tech-stack__title">TECH STACK</h3>
      <div class="app-tech-stack__container">
        <img v-for="tech in techStack" :key="tech.alt" :src="tech.src" :alt="tech.alt" class="app-tech-stack__item">
      </div>
    </section>

    <section class="app-contact">
      <h3 class="app-contact__title">CONTACT ME</h3>
      <ContactsForm class="app-contact__from"></ContactsForm>
      <div class="app-contact__social">
        <v-icon
          v-for="item in socials"
          :key="item.icon"
          class="app-contact__icon"
          @click="redirectTo(item.href)">{{ item.icon }}
        </v-icon>
      </div>
    </section>
  </div>
</template>

<script>
import ContactsForm from '~/components/ContactsForm'

export default {
  components: {
    ContactsForm
  },
  data() {
    return {
      socials: [
        {
          icon: 'mdi-facebook ',
          href: 'https://www.facebook.com/mimiroff',
        },
        {
          icon: 'mdi-at ',
          href: "mailto:ibarashkov@gmail.com",
        },
        {
          icon: 'mdi-phone ',
          href: "tel:+79263814022",
        }
      ],
      techStack: [
        {
          alt: 'Vue.js',
          src: '/vue-logo.svg'
        },
        {
          alt: 'Nuxt.js',
          src: '/nuxt-logo.svg'
        },
        {
          alt: 'Node.js',
          src: '/node-logo.svg'
        },
        {
          alt: 'Nest.js',
          src: '/nest-logo.svg'
        }
      ],
      aboutMe: {
        left: `Hi! I'm Ilya Barashkov, a software engineer in web development. I have loved coding for decades as a hobby. Now I love it even more as a profession. Since 2018 I'm working as a full-stack developer creating nicely and logically structured UI and API, building the reliable and efficient backend.`,
        right: `My way into the profession was fast and effective because I was lucky to have wonderful mentors. Now, as an act of acknowledgment, I am helping newcomers to get into web development with mentorship by myself and I'm trying my best to match my teachers.`
      }
    }
  },
  methods: {
    redirectTo(url) {
      window.location = url;
    },
    goToAboutMe() {
      this.$refs.about.scrollIntoView({
        behavior: 'smooth'
      })
    }
  }
}
</script>

<style lang="scss">
.app {
  &-home {
    height: 100vh;
    background-image: url("/notebook-gray.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: top center;
    min-width: $min-content-width;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    &__title {
      margin: 0;
      padding: 0;
      font-size: 72px;
      font-weight: 500;
      width: 100%;
      text-align: center;

      @media (max-width: $mobile-width) {
        font-size: 60px;
      }
    }

    &__icon {
      font-size: 72px!important;
      margin-top: 72px;
      border-radius: 50%;
    }
  }

  &-about {
    margin: 0 auto;
    padding: 72px 36px;
    max-width: $max-content-width;
    min-width: $min-content-width;
    font-size: 24px;
    font-weight: 500;

    &__title {
      margin: 0;
      padding: 0;
      text-align: center;
      font-size: 32px;
    }

    &__photo {
      width: 240px;
      height: 240px;
      border-radius: 50%;
      margin: 72px auto 0 auto;
      background-image: url("/photo.jpg");
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
    }

    &__text-container {
      margin-top: 72px;
      display: flex;
      flex-direction: row;
      align-items: flex-start;
      justify-content: space-between;

      @media (max-width: $mobile-width) {
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
      }
    }

    &__text {
      padding: 0;
      font-weight: 300;

      @media (max-width: $mobile-width) {
        text-align: justify;
        font-size: 20px;
      }

      &--right {
        margin-left: 32px;

        @media (max-width: $mobile-width) {
          margin-left: 0;
          margin-top: 16px;
        }
      }
    }
  }

  &-tech-stack {
    padding: 72px;
    background-image: url("/notebook-white.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: top center;
    background-attachment: fixed;
    min-width: $min-content-width;

    @media (max-width: $tablet-width) {
      padding: 72px 36px;
    }

    &__title {
      margin: 0;
      padding: 0;
      text-align: center;
      font-size: 32px;
      color: #000000;
    }

    &__container {
      display: flex;
      flex-direction: row;
      height: 100%;
      align-items: center;
      justify-content: space-between;
      margin-top: 60px;

      @media (max-width: $mobile-width) {
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
      }
    }

    &__item {
      width: 200px;
      height: 200px;

      @media (max-width: $tablet-width) {
        width: 150px;
        height: 150px;
      }
    }
  }

  &-contact {
    margin: 0 auto;
    padding: 72px 36px;
    max-width: $max-content-width;
    min-width: $min-content-width;
    font-size: 24px;
    font-weight: 500;

    &__title {
      margin: 0 0 60px 0;
      padding: 0;
      text-align: center;
      font-size: 32px;
    }

    &__social {
      margin: 60px auto 0 auto;
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      max-width: 600px;
    }

    &__icon {
      font-size: 48px!important;
    }
  }
}
</style>
