<template>
  <div class="article-container">
    <h2 class="title">{{emojComment(title)}}</h2>
    <div class="desc">
      <p
        class="paragragh"
        v-for="(p, index) in paragraphs"
        :key="index"
        v-html="emojComment(p)"
      ></p>
    </div>
    <div class="count">
      <span class="liked"><i class="icon-like2 iconfont"></i>{{liked_count}}</span>
      <span class="comments"><i class="icon-pinglun iconfont"></i> {{comments_count}}</span>
      <span class="collected"><i class="icon-shoucang iconfont"></i> {{collected_count}}</span>
    </div>
    <div
      class="time"
    >发布于 {{formatTime}}</div>
  </div>
</template>

<script>
import { setTime, emojComment } from '@/utils';

export default {
  data() {
    return {
    };
  },

  props: {
    title: String,
    description: {
      default: '',
      type: String,
    },
    ats: {
      default: () => [],
      type: Array,
    },
    liked_count: Number,
    collected_count: Number,
    comments_count: Number,
    time: String,
  },

  computed: {
    paragraphs() {
      const des = this.showAts();
      return des.split('\n');
    },

    formatTime() {
      return setTime(this.time);
    },
  },

  methods: {
    emojComment,

    showAts() {
      let des = this.description;
      this.ats.forEach((element) => {
        des = des.replace(`@${element.name}`, `<a href="#" style="text-decoration:none;color:cornflowerblue">@${element.name}</a>`);
      });
      return des;
    },
  },
};
</script>

<style lang="less" scoped>
.article-container {
  .title {
    font-size: 24px;
    font-weight: 500;
  }

  .desc {
    .paragragh {
      font-size: 14px;
      margin: 20px 0 0 0;
      line-height: 20px;
    }
  }

  .count {
    margin: 30px 0 0 0;

    span {
      margin-right: 24px;
      display: inline-block;
      color: rgb(121, 121, 122);

      .iconfont {
        font-size: 21px;
        color: rgb(235, 59, 59);
        margin-right: 6px;
      }
    }

  }

  .time {
    margin: 40px 0;
    color: rgb(172, 161, 161);
  }
}
</style>
