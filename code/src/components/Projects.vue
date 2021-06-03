<template>
  <section id="projects">
    <AnimateOnVisible name="fadeDown" :duration="1">
      <Title class="title" :title="content.metadata.title" :description="content.metadata.description" />
    </AnimateOnVisible>

    <div class="col-12 full-width justify-center">
      <article class="content text-center">
        <AnimateOnVisible class="timeline q-mx-auto" v-for="(post, index) in content.metadata.items" :key="index" name="fadeLeft" :duration="0.5">
          <vue-timeline-update
            :date="new Date(post.date)"
            :title="post.title"
            :description="post.content"
            :thumbnail="getImgUrl(post.image)"
            :color="post.color"
            :category="post.tag"
            icon="code"
          >
            <h2>담당 역할</h2>
            <p>{{ post.role }}</p>
            <h2>참여 인원</h2>
            <p>{{ post.num }}</p>
            <h2>기술 스택</h2>
            <q-chip outline dense color="amber-5" text-color="white" v-for="(skill, index) in post.skills" :key="'A' + index">
              {{ skill }}
            </q-chip>
            <h2>개발 내용</h2>
            <li v-for="(detail, index) in post.details" :key="'B' + index">{{ detail }}</li>
            <!-- <h2>성과 및 결과</h2> -->
            <!-- <li v-for="(result, index) in post.results" :key="index">{{result}}</li> -->
            <div class="button q-gutter-sm">
              <q-btn v-if="post.link" id="btn" outline rounded color="orange-6" icon="add_to_home_screen" type="a" :href="post.link" label="Link"/>
              <q-btn id="btn" outline rounded color="cyan-6" icon="fab fa-github" type="a" :href="post.github" label="GitHub"/>
            </div>
          </vue-timeline-update>
        </AnimateOnVisible>
      </article>
    </div>
  </section>
</template>

<script>
import Title from './Title.vue';

export default {
  name: 'Projects',
  props: ['content'],
  components: {
    Title,
  },
  methods: {
    getImgUrl(img) {
      if (img == undefined || img == '') return '';
      return require('../assets/img/projects/' + img);
    },
    timeForToday(value) {
      const today = new Date();
      const timeValue = new Date(value);

      const betweenTime = Math.floor((today.getTime() - timeValue.getTime()) / 1000 / 60);
      if (betweenTime < 1) return '방금전';
      if (betweenTime < 60) {
        return `${betweenTime}분전`;
      }

      const betweenTimeHour = Math.floor(betweenTime / 60);
      if (betweenTimeHour < 24) {
        return `${betweenTimeHour}시간전`;
      }

      const betweenTimeDay = Math.floor(betweenTime / 60 / 24);
      if (betweenTimeDay < 365) {
        return `${betweenTimeDay}일전`;
      }

      return `${Math.floor(betweenTimeDay / 365)}년전`;
    },
  },
};
</script>

<style scoped lang="scss">
@import '@/styles/constants.scss';

$linear: map-get($colors, dark);

#projects {
  background-color: lighten(map-get($colors, primary), 5%);
}

.title {
  color: map-get($colors, light);
}

/deep/ .text-wrapper {
  &:after {
    border-bottom: 1px solid map-get($colors, dark);
  }
}

.button {
  margin-top: 2em;
  #btn{
    text-decoration: none !important;
  }
}

article .inner {
  position: relative;
  display: inline-block;
  vertical-align: middle;
  z-index: 1;
}

.content {
  color: map-get($colors, light);
  margin-top: 30px;
  header {
    height: 100%;
    width: 70%;
  }
  h1 {
    font-size: 3rem;
  }
  h2 {
    font-size: 2rem;
  }
  p,
  li {
    color: #ffca28;
    font-size: 1.2em;
  }
  
}

.vertical-center {
  display: flex;
  align-items: center;
}

h1 {
  margin-top: 10px;
  margin-bottom: 20px;
}
</style>
