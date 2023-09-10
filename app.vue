<script setup>
import data from '~/assets/data.yaml'
useHead({
  title: data.name,
  meta: [
    {
      name: 'description',
      content: `The homepage of ${data.name}`,
    },
    {
      name: "google-site-verification",
      content: "I9VHWgYS9g3o8RUJ7ryB1hPoIcN9YK1bX1Ds7_uDIYE",
    },
  ],
})

useSeoMeta({
  title: data.name,
  ogTitle: data.name,
  description: `The homepage of ${data.name}`,
  ogDescription: `The homepage of ${data.name}`,
  ogImage: 'https://ernestchu.github.io/assets/images/profile.webp',
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <img :src="data.profilePic" alt="profile pic" id="profile-pic">
  <div id="profile">
    <h2>{{ data.name }}</h2>
    <p v-for="profile in data.profiles"><span v-html="profile"></span></p>
  </div>
  <p v-for="bio in data.bios"><span v-html="bio"></span></p>

  <hr>

  <div id="pubs">
    <h2>Publications</h2>
    <p>Please refer to my CV and <a href="https://scholar.google.com/citations?user=ijvH9xQAAAAJ" target="_blank">Google Scholar profile</a></p>
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
</template>

<style>
body {
  font-family: -apple-system,system-ui,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  color: #303030;
  background-color: #EAE9E4;
}

a {
  color: #303030;
  text-decoration: none;
  position: relative;
  white-space: nowrap;
  cursor: pointer;
}
a:after {
  content: '';
  position: absolute;
  z-index: -1;
  top: 66%;
  left: -0.1em;
  right: -0.1em;
  bottom: 0;
  transition: top 200ms cubic-bezier(0, 0.8, 0.13, 1);
  background-color: #8C151555;
}

@media (hover: hover) {
  a:hover:after {
    top: 0%;
  }
}
a:active:after {
  top: 0%;
}

p {
  font-size: 14pt;
}

hr {
  border: solid #D5D0C0 1px;
}

div#app {
  margin: 0 10%;
  padding-bottom: 50px;
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
  width: 250px;
}
@media (max-width: 800px) {
img#profile-pic {
  display: none;
}
}

div#projects div.link {
  display: inline;
  margin-right: 5px;
}

div#projects img {
  width: 200px;
}

div#projects .contents {
  vertical-align: top;
  margin-left: 20px;
  display: inline-block;
  max-width: calc(100% - 220px);
}

@media (max-width: 800px) {
div#projects img {
  display: none;
}
div#projects .contents {
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
