<template>
  <div class="profile-page">
    <Banner>
      <div class="text-center">
        <h1 class="text-white text-smooth text-shadow">
          <b>Enal Farid</b>
        </h1>
        <h5 class="text-white text-smooth text-shadow">
          Hi, I am Enal Farid a Product Manager and Full Stack Developer.”
        </h5>
      </div>
    </Banner>
    <section class="section section-skew">
      <div class="container">
        <Card shadow class="card-profile" no-body>
          <div class="px-4">
            <div class="row justify-content-center">
              <div class="col-lg-3 order-lg-2">
                <div class="card-profile-image">
                  <a href="#me" aria-hidden="true">
                    <img v-lazy="'/assets/img/collections/enal-mandiriwtf.png'" class="rounded-circle" alt="Enal Farid">
                  </a>
                </div>
              </div>
              <div class="col-lg-4 order-lg-3 text-lg-right align-self-lg-center">
                <div class="card-profile-actions py-4 mt-lg-0">
                  <Button
                    tag="a"
                    target="_blank"
                    rel="noreferrer"
                    href="/media/resume-enalfarid.pdf"
                    type="info"
                    size="sm"
                    class="mr-4"
                  >
                    <client-only>
                      <md-briefcase-icon w="14px" h="14px" />
                    </client-only>
                    Resume
                  </Button>
                  <Button
                    tag="a"
                    type="primary"
                    class="float-right"
                    size="sm"
                    href="mailto:farid.enal@gmail.com"
                  >
                    <client-only>
                      <md-mail-icon w="14px" h="14px" />
                    </client-only>
                    Contact
                  </Button>
                </div>
              </div>
              <div class="col-lg-4 order-lg-1">
                <div class="card-profile-stats d-flex justify-content-center">
                  <div>
                    <span class="heading">
                      <span v-if="github.ready">{{ github.contributions }}</span>
                      <md-help-circle-outline-icon v-else w="18px" h="18px" animate="beat" />
                    </span>
                    <span class="description">Contributions</span>
                  </div>
                  <div>
                    <span class="heading">
                      <span v-if="github.ready">{{ github.publicRepos }}</span>
                      <md-help-circle-outline-icon v-else w="18px" h="18px" animate="beat" />
                    </span>
                    <span class="description">Repositories</span>
                  </div>
                  <div>
                    <span class="heading">
                      <span v-if="github.ready">{{ github.publicGists }}</span>
                      <md-help-circle-outline-icon v-else w="18px" h="18px" animate="beat" />
                    </span>
                    <span class="description">Gists</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="text-center mt-5">
              <h3>
                Enal Farid
              </h3>
              <div class="h6 font-weight-300">
                Makassar, Indonesia
              </div>
              <div class="h6 mt-4">
                Product Manager, Full Stack Developer
              </div>
              <div>
                Lintas Inovasi Digital
              </div>
            </div>
            <div class="mt-5 py-4 border-top text-center">
              <div class="row justify-content-center">
                <div class="col-lg-9">
                  <h2 class="text-smooth">
                    About
                  </h2>
                  <p>
                    <client-only>
                      <md-quote-icon w="14px" h="14px" />
                    </client-only>
                    Product Manager who implement bussiness idea in to application, but have
                    an ability as Full Stack Developer. Very passionate about
                    modern mobile and web technology using JavaScript while taking into
                    consideration the latest trends and techniques.
                  </p>
                </div>
              </div>
              <h2 class="mt-5 text-smooth">
                Coding Activities
              </h2>
              <div class="row py-4">
                <div class="col-md-6">
                  <figure>
                    <embed src="https://wakatime.com/share/@7a831ab0-e43a-4215-aa08-92f915bed065/6309a505-c658-470e-a5ae-266aa8684053.svg">
                  </figure>
                </div>
                <div class="col-md-6">
                  <figure>
                    <embed src="https://wakatime.com/share/@7a831ab0-e43a-4215-aa08-92f915bed065/c584e591-eec6-4df1-81ad-e2930e1e5c6e.svg">
                  </figure>
                </div>
              </div>
            </div>
          </div>
        </Card>
      </div>
    </section>
  </div>
</template>

<script>
import MdBriefcaseIcon from 'vue-ionicons/dist/md-briefcase.vue'
import MdHelpCircleOutlineIcon from 'vue-ionicons/dist/md-help-circle-outline.vue'
import MdMailIcon from 'vue-ionicons/dist/md-mail.vue'
import MdQuoteIcon from 'vue-ionicons/dist/md-quote.vue'
import Card from '~/components/Argon/Card'
import Button from '~/components/Argon/Button'
import Banner from '~/components/Base/Banner'
import { metaGenerator } from '~/utils/helpers'

export default {
  components: {
    Banner,
    Card,
    Button,
    MdMailIcon,
    MdQuoteIcon,
    MdHelpCircleOutlineIcon,
    MdBriefcaseIcon
  },
  data: () => ({
    github: {
      ready: false,
      contributions: 0,
      publicRepos: 0,
      publicGists: 0
    }
  }),
  mounted() {
    Promise.all([
      window.fetch('https://api.github.com/users/enalfarid')
        .then(res => res.json())
        .then(res => res),
      window.fetch('https://github-contributions-api.now.sh/v1/enalfarid')
        .then(res => res.json())
        .then(({ years }) => years.reduce((acc, cur) => acc + cur.total, 0))
    ]).then(result => {
      this.github.ready = true
      this.github.publicRepos = result[0].public_repos
      this.github.publicGists = result[0].public_gists
      this.github.contributions = result[1]
    })
  },
  head: () => ({
    title: `${process.env.AUTHOR}`,
    meta: metaGenerator('portfolio', {
      title: 'Personal Homepage',
      description: `A Product Manager who love coffee and coding. - ${process.env.AUTHOR}`,
      keywords: 'homepage, portfolio',
      image: '/icon.png',
      url: '/'
    })
  })
}
</script>
