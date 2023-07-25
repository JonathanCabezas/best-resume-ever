<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">
        <p v-for="p in person.position" v-html="p">
        </p>
      </div>
      <div v-if="person.birth" class="banner__location">{{ lang.born }} {{person.birth.year}}</div>
    </div>

    <div class="content">
      <div class="content__left">


        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain section-content--contact section-content__left">
            <div class="section-link">
              <i class="section-link__icon material-icons">business</i>
              <ul class="quicklist">
                <li>{{person.contact.street}}</li>
                <li>{{person.contact.city}}</li>
              </ul>
            </div>

            <a
              class="section-link link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <a
              v-if="person.contact.website"
              class="section-link link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>

            <a
              v-if="person.contact.linkedin"
              class="section-link link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>

            <a
              v-if="person.contact.github"
              class="section-link link"
              :href="contactLinks.github">
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>

            <a
              v-if="person.contact.medium"
              class="section-link link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>


        <div
          v-if="person.skills"
          class="section">
          
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div
            v-for="(skills, index1) in person.skills"
            :key="index1"
            class="section">
            <div>
              {{ skills.category }}
            </div>

            <div class="section-content-grid">
                <a
                  v-for="(skill,index2) in skills.list"
                  class="grid-item"
                  :key="index2"
                  :href="skill.url">
                  <span class="squarred-grid-item-left">
                    {{ skill.name }}
                  </span>
                </a>
            </div>
          </div>
        </div>

        <div
          v-if="person.softs"
          class="section">
          <div class="section-headline">
            {{ lang.softs }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.softs"
              class="grid-item"
              :key="index"
              :class="{ link: skill.url !== undefined}"
              :href="skill.url">
              <span class="squarred-grid-item-left">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.certifications"
          class="section">
          <div class="section-headline">
            {{ lang.certifications }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(cert, index) in person.certifications"
              class="grid-item"
              :key="index"
              :href="cert.url">
              <span class="squarred-grid-item-left">
                {{ cert.name }}
              </span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            {{ lang.about }}
          </div>

          <div class="section-content section-content--plain section-content__left">
            <ul>
              <li class="about" v-for="a in person.about" v-html="a"></li>
            </ul>
          </div>
        </div>

        </div>
      </div>

      <div class="content__right">

        <div class="section">
          <div class="section">
            <div class="section-headline">
              <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
            </div>

            <div class="section-content">
              <a
                v-for="(experience, index) in person.experience"
                :key="index"
                class="section-content__item"
                :class="{ link: experience.website !== undefined}"
                :href="experience.website">

                <span class="section-content__header">{{ experience.position }}</span>
                <span class="section-content__subheader">
                  {{ experience.company }}
                  <span class="section-content__plain">{{ experience.location }}</span>
                </span>

                <div class="section-content__text">{{ experience.timeperiod }}</div>
                <ul>
                  <li 
                    v-for="desc in experience.description"
                    class="section-content__text--light">
                    {{ desc }}
                  </li>
                </ul>
              </a>
            </div>
          </div>

          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>

          <div class="section-content">
            <a
              v-for="(education, index) in person.education"
              class="section-content__item"
              :key="index"
              :class="{ link: education.website !== undefined}"
              :href="education.website">

              <span class="section-content__header"> {{ education.degree }} </span>
              <span class="section-content__subheader">{{ education.school }}</span>
              <span class="section-content__text"> {{ education.timeperiod }} </span>
              <span class="section-content__text--light"> {{ education.description }} </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.projects"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">code</i>{{ lang.projects }}
          </div>

          <div class="section-content-grid section-content-grid--projects">
            <a v-for="(project, index) in person.projects" :key="index"
              class="grid-item"
              :class="{ link: project.url !== undefined}"
              :href="project.url">
              <span class="squarred-grid-item-right">
                <span class="section-content__header" v-html="project.name"></span>
                <span class="section-content__subheader">{{ project.platform }}</span>
                <span class="section-content__text"> {{ project.description }} </span>
              </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.contributions"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-heart"></i>{{lang.contributions}}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(contribution, index) in person.contributions"
              class="section-content__item-grid"
              :key="index"
              :class="{ link: contribution.url !== undefined}"
              :href="contribution.url">
              <span class="section-content__header"> {{ contribution.name }} </span>
              <span class="section-content__text"> {{ contribution.description }} </span>
              <span class="section-content__text--light" style="word-break: break-all;">
                {{ contribution.url }}
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <img class="picture"/>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'cool';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less">
@accent-color: #34495E;
@banner-color: #42b883;
@highlight-color: @banner-color;
@text-light-color: white;
@text-dark-color: rgba(255, 255, 255, 0.59);
@banner-height: 90px;
@picture-border-color: white;
@picture-size: 160px;
@picture-top-offset: 20px;
@picture-right-offset: 20px;
@base-padding: 20px;
@left-column-width: 240px;

.highlightedText {
    color:@highlight-color;
}

.link {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}


.quicklist {
  margin:0;
  padding:0 !important;
  list-style-type:none;
}

ul {
  margin: 6px 0 0 0;
  padding: 0 0 0 30px;
}

.content__left ul {
  padding: 0 0 0 15px;
}

.about {
  margin: 6px 0 0 0;
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.picture {
  position: absolute;
  top: @picture-top-offset;
  right: @picture-right-offset;
  height: @picture-size;
  width: @picture-size;
  border-radius: 2%;
  border: 2px solid @picture-border-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  color: @text-light-color;

  &__fullname {
    font-size: 34px;
  }

  &__position {
    font-size: 20px;
  }

  &__location {
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;
  box-shadow: 10px 5px 10px black;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
    padding-top: @base-padding / 3;
  }

  &__left {
    width: @left-column-width;
    color: @text-dark-color;
    background-color: @accent-color;

    .section-headline {
      color: @text-light-color;
      font-size: 18px;
    }
  }

  &__right {
    flex: 1;
    background-color: @text-light-color;
  }
}

.section {
  margin: 18px 0;
}

/* Lower margins for the first section */
.content__left > .section .section:nth-of-type(2) {
  margin: 10px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 18px;
  margin: 0 0 5px;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: @text-dark-color;

  &__icon {
    color: @text-light-color;
  }
}

/*
 Grille droite, plus de marge à gauche
 Image à remettre en carré blanc en haut à droite
 Image plus grande
 Trop de marge à droite (bullet point sur une ligne, notamment responsable de cours etc)
 Remettre section de gauche en 240px
 */

.section-content {
  margin-top: 5px;
  padding-left: 16px;
  font-size: 14px;

  &__left {
    margin-top: 10px;
  }

  &__item {
    display: block;
    margin-bottom: 8px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
    margin-bottom: 2px;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }

  &--contact {
    margin-left: 5px;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin: 5px 0 5px 5px;

  &--projects {
    margin-left: 28px;
  }
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item-left {
  display: block;
  border: 1px solid @text-light-color;
  color: @text-light-color;
  margin-top: 5px;
  padding: 5px;
}

.squarred-grid-item-right {
  font-size: 13px;
  display: block;
  border: 1px solid black;
  color: black;
  margin-top: 6px;
  padding: 5px;
}
</style>
