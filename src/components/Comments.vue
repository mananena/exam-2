<template>
  <ul class="section" v-if="comments.length > 0">
    <Comment
      @showDialog="changeParentCommentId"
      v-for="comment in nestedComments"
      :comment="comment"
      :childs="comment.childs"
      :key="comment.id"
      class="section__item"
      st
    />
  </ul>
  <p class="section-text" v-else>Комментариев не найдено</p>
</template>

<script>
import Comment from './Comment.vue';

export default {
  components: { Comment },
  props: {
    comments: {
      type: Array,
      required: true,
    },
  },
  computed: {
    nestedComments() {
      let nestedComments = [];
      this.comments.forEach((comment) => {
        if (comment.parentId === null || !comment.parentId) {
          let commentChanged = { ...comment };
          commentChanged.childs = this.findChilds(
            commentChanged,
            this.comments
          );
          nestedComments.push(commentChanged);
        }
      });
      return nestedComments;
    },
  },
  methods: {
    findChilds(parent, arr) {
      let childs = arr.filter((comment) => comment.parentId === parent.id);
      if (childs.length === 0) return null;
      childs.forEach((childComment) => {
        childComment.childs = this.findChilds(childComment, this.comments);
      });
      return childs;
    },
    changeParentCommentId(parentCommentId) {
      console.log(parentCommentId);
      this.$emit('reply', parentCommentId);
    },
  },
};
</script>

<style scoped lang="scss">
@use '@/assets/scss/mixin' as *;
.section {
  margin-top: 1.5rem;
}
.section-text {
  @include subTitle();
}
</style>