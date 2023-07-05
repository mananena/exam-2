<template>
  <li class="comment">
    <div class="comment__comment" :class="colorReaction">
      <p class="comment__author">
        {{ comment.author }}
      </p>
      <p class="comment__text">
        {{ comment.text }}
      </p>
      <div class="comment__bottom">
        <my-button class="comment__button" @click="showDialog">
          Ответить</my-button
        >
        <span class="comment__replies" v-if="childs">
          <svg
            version="1.1"
            id="Layer_1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            width="32px"
            height="32px"
            viewBox="0 0 32 32"
            enable-background="new 0 0 32 32"
            xml:space="preserve"
          >
            <path
              id="mail"
              fill="#333333"
              d="M28,5H4C1.791,5,0,6.792,0,9v13c0,2.209,1.791,4,4,4h24c2.209,0,4-1.791,4-4V9
              C32,6.792,30.209,5,28,5z M2,10.25l6.999,5.25L2,20.75V10.25z M30,22c0,1.104-0.898,2-2,2H4c-1.103,0-2-0.896-2-2l7.832-5.875
              l4.368,3.277c0.533,0.398,1.166,0.6,1.8,0.6c0.633,0,1.266-0.201,1.799-0.6l4.369-3.277L30,22L30,22z M30,20.75l-7-5.25l7-5.25
              V20.75z M17.199,18.602c-0.349,0.262-0.763,0.4-1.199,0.4c-0.436,0-0.851-0.139-1.2-0.4L10.665,15.5l-0.833-0.625L2,9.001V9
              c0-1.103,0.897-2,2-2h24c1.102,0,2,0.897,2,2L17.199,18.602z"
            />
            <path
              style="fill: #6770e6"
              d="M95 94H16C7.163 94 0 86.837 0 78s7.163-16 16-16h79v32z"
            />
            <path
              d="M16 62C7.163 62 0 69.163 0 78c0 1.026.106 2.027.291 3C1.696 73.599 8.19 68 16 68h79v-6H16z"
              style="fill: #858eff"
            />
            <path
              style="fill: #6770e6"
              d="M95 144H26c-8.837 0-16-7.163-16-16s7.163-16 16-16h69v32zM95 194H46c-8.837 0-16-7.163-16-16s7.163-16 16-16h49v32z"
            />
            <path
              d="M30.291 175a16.035 16.035 0 0 0-.291 3c0 8.837 7.163 16 16 16h49v-6H46c-7.81 0-14.304-5.599-15.709-13z"
              style="fill: #5861c7"
            />
            <path
              d="M240 194H88c-8.837 0-16-7.163-16-16V78c0-8.837 7.163-16 16-16h152c8.837 0 16 7.163 16 16v100c0 8.837-7.163 16-16 16z"
              style="fill: #69ebfc"
            />
            <path
              style="fill: #5fd4e3"
              d="M240 187H88c-8.837 0-16-7.163-16-16v7c0 8.837 7.163 16 16 16h152c8.837 0 16-7.163 16-16v-7c0 8.837-7.163 16-16 16z"
            />
            <path
              d="M240 62H88c-8.837 0-16 7.163-16 16v6c0-8.837 7.163-16 16-16h152c8.837 0 16 7.163 16 16v-6c0-8.837-7.163-16-16-16z"
              style="fill: #a1f1fc"
            />
            <path
              style="fill: #5fd4e3"
              d="M172.397 153.197a12.437 12.437 0 0 1-16.794 0L72 76.691v14.735l75.73 69.302 7.922 7.217a12.42 12.42 0 0 0 15.87.128l7.928-7.21 76.368-69.886c.061-.082.121-.169.181-.252V79.026c0-.744-.064-1.472-.157-2.192l-83.445 76.363z"
            />
          </svg>
          {{ childs.length }}
        </span>
        <time class="comment__date">
          {{ convertDate }}
        </time>
      </div>
    </div>
    <ul v-if="childs" class="comment__childs">
      <Comment
        @showDialog="showChildDialog"
        v-for="child in childs"
        :comment="child"
        :childs="child.childs"
        :key="child.id"
        :style="{
          'margin-left': 10 + 'px',
        }"
      />
    </ul>
  </li>
</template>

<script>
export default {
  props: {
    comment: {
      typeof: Object,
      required: true,
    },
    childs: {
      typeof: Array,
    },
  },
  data() {
    return {
      repliesShow: true,
      date: this.comment.createdAt,
    };
  },
  computed: {
    colorReaction() {
      if (!this.childs) return;
      let sum = 0;
      this.childs.forEach((comment) => {
        sum += comment.reaction;
      });
      if (sum > 0) {
        return "item__positive";
      } else if (sum < 0) {
        return "item__negative";
      }
      return;
    },
    convertDate() {
      return new Intl.DateTimeFormat("ru", {
        year: "numeric",
        month: "numeric",
        day: "numeric",
        hour: "numeric",
        minute: "numeric",
      }).format(Date.parse(this.date));
    },
  },
  methods: {
    updateCheck() {
      this.repliesShow = !this.repliesShow;
    },
    showChildDialog(id) {
      this.$emit("showDialog", id);
    },
    showDialog() {
      this.$emit("showDialog", this.comment.id);
    },
  },
};
</script>

<style scoped lang="scss">
@use "@/assets/scss/mixin" as *;
@use "@/assets/scss/function" as *;
@use "@/assets/scss/variables" as *;
.comment__childs {
  border-left: #e4e4e4 0.5rem solid;
}
.comment__comment {
  padding: 1rem;
  margin-top: 1rem;
  list-style: none;
  border-radius: 5px;
  background-color: #e4e4e4;
  transition: box-shadow 0.8s linear;
  @include media(min, md) {
    padding: 15px;
  }
  &:hover {
    box-shadow: 0px 0px 3px 0px #bebbbb;
  }
}
.comment__positive {
  background-color: #46d38d52;
}
.comment__negative {
  background-color: #ff686852;
}
.comment__author {
  font-size: 2rem;
  font-weight: 600;
  word-break: break-word;
}
.comment__text {
  margin-top: 1rem;
  font-size: 1.6em;
  word-break: break-word;
}
.comment__svg {
  height: 2rem;
}
.comment__bottom {
  margin-top: 15px;
  display: flex;
  align-items: center;
}
.comment__button {
  font-size: 1.2rem;
  font-weight: 600;
  @include media(min, md) {
    font-size: 1.2rem;
  }
}
.comment__replies {
  margin-left: auto;
  font-size: 1.4rem;
  line-height: 1;
  display: flex;
  align-items: center;
  gap: 5px;
}
.comment__replies + .comment__date {
  @include media(min, xs) {
    margin-left: 15px;
  }
}
.comment__date {
  margin-left: auto;
  font-size: 1.4rem;
  line-height: 1;
}
</style>