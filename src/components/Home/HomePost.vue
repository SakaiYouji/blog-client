<template>
  <section :class="$style['article']">
    <header :class="$style['header']">
      <h4>推荐文章</h4>
      <router-link :class="$style['header-link']" to="/posts" >更多文章</router-link>
    </header>
    <ul>
      <li
        v-for="item in recommendPosts"
        :class="$style['main-item']"
        :style="{'background-image': `url(${item.imgUrl})`}"
        :key="item._id"
        @click="$router.push(`/posts/${item._id}`)"
      >
        <p :class="$style['main-item-txt']">{{ item.title }}</p>
        <span :class="$style['main-item-category']">{{ item.titleData }}</span>
      </li>
    </ul>
  </section>
</template>

<script>
import { getUrlWithWebp } from '@/utils/util'

export default {
  computed: {
    recommendPosts() {
      return this.$store.getters.getRecommendPosts
        .map(item => Object.assign(item, { imgUrl: getUrlWithWebp(item.imgUrl) }))
    }
  }
}
</script>

<style module lang="postcss">
.article {
  box-sizing: border-box;
  padding: 10px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 4px;
  line-height: 20px;
  cursor: default;
}

.header-link {
  font-size: 1em;

  &::after {
    margin-left: 2px;
    content: '>';
  }
}

.main-item {
  position: relative;
  margin: 10px 0;
  border-radius: 4px;
  text-align: center;
  color: white;
  background-position: 50% 50%;
  background-size: cover;
  background-repeat: no-repeat;
}

.main-item-txt {
  position: relative;
  box-sizing: border-box;
  padding: 0 30px;
  border-radius: 4px;
  overflow: hidden;
  font-size: 1.5em;
  line-height: 100px;
  text-overflow: ellipsis;
  white-space: nowrap;
  background-color: rgba(0, 0, 0, .3);
  cursor: pointer;
}

.main-item-category {
  position: absolute;
  bottom: 10px;
  right: 10px;
  display: inline-block;
  padding: 2px 4px;
  border-radius: 6px;
  font-size: 1em;
  line-height: 1.5;
  background: rgba(7, 17, 27, .4);
}

@media all and (min-width: 900px) {
  .main-item-txt {
    line-height: 160px;
  }
}
</style>
