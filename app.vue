<script setup>
import plain_data from '~/assets/data.yaml'
import { onMounted, nextTick, reactive } from 'vue'

const data = reactive(plain_data)

useHead({
  title: data.name,
  link: [
    { rel: 'stylesheet', href: 'https://use.typekit.net/vxy8tas.css' },
    { rel: 'stylesheet', href: 'https://use.typekit.net/jge8wgr.css' },
  ],
  meta: [
    {
      name: 'description',
      content: `The homepage of ${data.name}`,
    },
    {
      name: "google-site-verification",
      content: "1YldIPrKcx2CvMSIU19VVysjc4Eq2YtWhCnaY6Uc64U",
    },
  ],
})

useSeoMeta({
  title: data.name,
  ogTitle: data.name,
  description: `The homepage of ${data.name}`,
  ogDescription: `The homepage of ${data.name}`,
  ogImage: 'https://www.cs.jhu.edu/~schu23/images/profile.webp',
  twitterCard: 'summary_large_image',
})


onMounted(() => {
})
</script>

<template>
  <div id="app">
    <img src="/images/profile.webp" alt="profile pic" id="profile-pic">
    <div id="profile">
      <div class="myname">{{ data.name }}</div>
      <div v-for="profile in data.profiles"><span v-html="profile"></span></div>
    </div>
    <p v-for="bio in data.bios"><span v-html="bio"></span></p>

    <hr>

    <div id="pubs">
      <h2>Selected Publications</h2>
      <div class="project" v-for="pub in data.publications">
        <h3>{{ pub.title }}</h3>
        <div class="contents">
          <div v-html="pub.authors"></div>
          <h4>{{ pub.venue }}</h4>
          <div class="link">
            [<a @click="pub.show_abstract = !pub.show_abstract">
              {{ pub.show_abstract ? 'Hide' : 'Show' }} abstract
            </a>]
          </div>
          <div class="link" v-for="[linkName, link] in Object.entries(pub.links)">
            [<a :href="link" target="_blank">{{ linkName }}</a>]
          </div>
          <p v-if="pub.show_abstract">{{ pub.abstract }}</p>
        </div>
        <hr>
      </div>
      <p>Please refer to my CV and <a href="https://scholar.google.com/citations?user=ijvH9xQAAAAJ"
          target="_blank">Google Scholar profile</a> for a full list.</p>
    </div>

    <hr>

    <div id="projects">
      <h2>Selected Projects</h2>
      <div class="project" v-for="project in data.projects">
        <h3>{{ project.title }}</h3>
        <!-- <img :src="project.thumbnail ? project.thumbnail : defaultThumbnail" alt="project thumbnail" loading="lazy"> -->
        <div class="contents">
          <ul>
            <li v-for="description in project.descriptions">{{ description }}</li>
          </ul>
          <div class="link" v-for="[linkName, link] in Object.entries(project.links)">
            [<a :href="link" target="_blank">{{ linkName }}</a>]
          </div>
        </div>
        <hr>
      </div>
    </div>

    <!--
    <a href="cse435-introduction-to-electronic-design-automation-and-testing/hw5/hw5.pdf" class="hide">print</a>
    -->
  </div>
</template>

<style>
body {
  /*font-family: -apple-system,system-ui,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;*/
  font-family: "proxima-nova", sans-serif;
  color: #303030;
  background-color: #f6f6f5;
}

h2 {
  font-family: "factoria", sans-serif;
  font-weight: 700;
  font-size: 20pt;
}

a {
  color: #303030;
  text-decoration: none;
  position: relative;
  white-space: nowrap;
  cursor: pointer;
  transition: all 500ms cubic-bezier(0, 0.8, 0.13, 1);
}

a:after {
  content: '';
  position: absolute;
  z-index: -1;
  top: 66%;
  left: -0.1em;
  right: -0.1em;
  bottom: 0;
  transition: all 500ms cubic-bezier(0, 0.8, 0.13, 1);
  background-color: #68ACE5bb;
}

@media (hover: hover) {
  a:hover {
    color: #fff;
  }

  a:hover:after {
    top: 0%;
    background-color: #002D72;
  }
}

a:hover {
  color: #fff;
}

a:active:after {
  top: 0%;
  background-color: #002D72;
}

hr {
  border: solid #D5D0C0 1px;
}

div#app {
  margin: 0 10%;
  padding-bottom: 50px;
}

.myname {
  margin: 30px 0 35px 0;
  font-family: "factoria", sans-serif;
  font-weight: 700;
  font-size: 30pt;
}

div#profile {
  vertical-align: top;
  padding: 0 20px;
  display: inline-block;
  max-width: calc(100% - 300px);
}

@media (max-width: 800px) {
  div#profile {
    padding: initial;
    max-width: initial;
  }
}

img#profile-pic {
  padding: 15px 0;
  width: 220px;
}

/*
@media (max-width: 800px) {
img#profile-pic {
  display: none;
}
}
*/

div#projects div.link,
div#pubs div.link {
  display: inline;
  margin-right: 5px;
}

div#projects img,
div#pubs img {
  width: 200px;
}

div#projects .contents,
div#pubs .contents {
  vertical-align: top;
  margin-left: 20px;
  display: inline-block;
  max-width: calc(100% - 220px);
}

@media (max-width: 800px) {

  div#projects img,
  div#pubs img {
    display: none;
  }

  div#projects .contents,
  div#pubs .contents {
    vertical-align: initial;
    margin-left: initial;
    display: initial;
    max-width: initial;
  }
}

.hide {
  opacity: 0;
  transition: opacity .3s;
}

.hide:hover {
  opacity: 1;
}
</style>
