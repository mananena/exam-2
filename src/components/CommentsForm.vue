<template>
  <form method="post" class="form" @submit.prevent="createComment">
    <label class="form__label">
      <span class="form__text">Введите ваше имя</span>
      <my-input
        v-model.trim="formData.author"
        class="form__input"
        inputType="text"
        inputName="author"
        placeholder="Ваше имя"
        required
      />
    </label>
    <label class="form__label">
      <span class="visually-hidden">Введите текст комментарий</span>
      <my-textarea
        v-model="formData.text"
        class="form__input"
        textareaName="text"
        placeholder="Текст комментария"
        rows="7"
        required
      ></my-textarea>
    </label>
    <label class="form__label">
      <span class="visually-hidden">Нравится</span>
      <input
        v-model="formData.reaction"
        type="radio"
        name="reaction"
        value="1"
        class="form__radio visually-hidden"
        required
      />
      <svg class="form__img"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 50 50"
        width="22"
        height="22"
      >
        <defs></defs>
        <path
          fill="#ffe500"
          d="M3.684 26.486a21.316 19.502 0 1 0 42.632 0 21.316 19.502 0 1 0-42.632 0"
        ></path>
        <path
          d="M25 42.357c-12.062 0-20.324-7.768-21.226-17.687-.055.6-.09 1.2-.09 1.816 0 10.77 8.526 19.5 21.316 19.5s21.316-8.732 21.316-19.5c0-.613-.035-1.217-.09-1.816-.902 9.919-9.164 17.687-21.226 17.687z"
          fill="#f2c100"
        ></path>
        <path
          fill="#fffacf"
          d="M19.104 9.253a5.896.908 0 1 0 11.792 0 5.896.908 0 1 0-11.792 0"
        ></path>
        <path
          stroke-miterlimit="10"
          stroke="#45413c"
          stroke-width="1.25"
          fill="none"
          d="M3.684 26.486a21.316 19.502 0 1 0 42.632 0 21.316 19.502 0 1 0-42.632 0"
        ></path>
        <path
          d="M21.023 24.358a1 1 0 0 1 1-.941h5.959a1 1 0 0 1 1 .94c.116 1.951-.071 6.26-3.977 6.26s-4.098-4.307-3.982-6.259z"
          stroke-linecap="round"
          stroke-linejoin="round"
          fill="#ff6242"
          stroke="#45413c"
          stroke-width="1.25"
        ></path>
        <path
          d="M3.981 11.63a5.828 5.828 0 0 1 9.053-5.8 5.828 5.828 0 0 1 10.484 2.388c1.2 6.9-7.761 13.2-7.761 13.2S5.185 18.526 3.981 11.63z"
          fill="#ff6196"
        ></path>
        <path
          d="M18.329 6.834a5.824 5.824 0 0 0-3.723 1.386 2.242 2.242 0 0 1-2.239.391 5.825 5.825 0 0 0-3.973-.042A5.733 5.733 0 0 0 4.546 13.4a7.566 7.566 0 0 1-.565-1.767 5.828 5.828 0 0 1 9.053-5.8 5.828 5.828 0 0 1 10.484 2.385 7.508 7.508 0 0 1 .067 1.854 5.731 5.731 0 0 0-5.256-3.238z"
          fill="#ff87af"
        ></path>
        <path
          d="M3.981 11.63a5.828 5.828 0 0 1 9.053-5.8 5.828 5.828 0 0 1 10.484 2.388c1.2 6.9-7.761 13.2-7.761 13.2S5.185 18.526 3.981 11.63z"
          fill="none"
          stroke="#45413c"
          stroke-width="1.25"
          stroke-linecap="round"
          stroke-linejoin="round"
        ></path>
        <path
          d="M46.019 11.63a5.828 5.828 0 0 0-9.053-5.8 5.828 5.828 0 0 0-10.484 2.388c-1.2 6.9 7.761 13.2 7.761 13.2s10.572-2.892 11.776-9.788z"
          fill="#ff6196"
        ></path>
        <path
          d="M31.671 6.834a5.824 5.824 0 0 1 3.723 1.386 2.242 2.242 0 0 0 2.239.391 5.825 5.825 0 0 1 3.973-.042 5.733 5.733 0 0 1 3.848 4.831 7.566 7.566 0 0 0 .565-1.767 5.828 5.828 0 0 0-9.053-5.8 5.828 5.828 0 0 0-10.484 2.385 7.508 7.508 0 0 0-.067 1.854 5.731 5.731 0 0 1 5.256-3.238z"
          fill="#ff87af"
        ></path>
        <path
          d="M46.019 11.63a5.828 5.828 0 0 0-9.053-5.8 5.828 5.828 0 0 0-10.484 2.388c-1.2 6.9 7.761 13.2 7.761 13.2s10.572-2.892 11.776-9.788z"
          fill="none"
          stroke="#45413c"
          stroke-width="1.25"
          stroke-linecap="round"
          stroke-linejoin="round"
        ></path>
      </svg>
    </label>
    <label class="form__label">
      <span class="visually-hidden"> Нейтрально </span>
      <input
        v-model="formData.reaction"
        type="radio"
        required
        name="reaction"
        value="0"
        class="form__radio visually-hidden"
        checked
      />
      <svg class="form__img"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 50 50"
        width="22"
        height="22"
      >
        <defs></defs>
        <path
          fill="#ffe500"
          d="M1.5 25a23.5 21.5 0 1 0 47 0 23.5 21.5 0 1 0-47 0"
        ></path>
        <path
          d="M25 42.5C11.7 42.5 2.594 33.933 1.6 23c-.06.659-.1 1.325-.1 2 0 11.874 9.4 21.5 23.5 21.5S48.5 36.874 48.5 25c0-.676-.039-1.342-.1-2-.994 10.933-10.1 19.5-23.4 19.5z"
          fill="#f2c100"
        ></path>
        <path
          fill="#fffacf"
          d="M18.5 6.002a6.5 1.001 0 1 0 13 0 6.5 1.001 0 1 0-13 0"
        ></path>
        <path
          stroke-width="1.25"
          stroke-miterlimit="10"
          fill="none"
          stroke="#45413c"
          d="M1.5 25a23.5 21.5 0 1 0 47 0 23.5 21.5 0 1 0-47 0"
        ></path>
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          fill="#ff87af"
          stroke="#ff6196"
          stroke-width="1.25"
          d="M11 25.118a3.043 2.435 0 1 0 6.086 0 3.043 2.435 0 1 0-6.086 0"
        ></path>
        <path
          d="M20.739 25.118s1.065 1.3 4.261 1.3 4.261-1.3 4.261-1.3M15.87 18.422a2.435 2.435 0 1 1 4.869 0"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="1.25"
          fill="none"
          stroke="#45413c"
        ></path>
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          fill="#ff87af"
          stroke="#ff6196"
          stroke-width="1.25"
          d="M32.914 25.118a3.043 2.435 0 1 0 6.086 0 3.043 2.435 0 1 0-6.086 0"
        ></path>
        <path
          d="M34.13 18.422a2.435 2.435 0 1 0-4.869 0"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="1.25"
          fill="none"
          stroke="#45413c"
        ></path>
      </svg>
    </label>
    <label class="form__label">
      <span class="visually-hidden">Не нравится</span>
      <input
        v-model="formData.reaction"
        type="radio"
        name="reaction"
        value="-1"
        class="form__radio visually-hidden"
        required
      />
      <svg class="form__img"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 50 50"
        width="22"
        height="22"
      >
        <defs></defs>
        <path
          fill="#ffe500"
          d="M1.5 25.552a23.5 21.5 0 1 0 47 0 23.5 21.5 0 1 0-47 0"
        ></path>
        <path
          d="M25 43.049c-13.3 0-22.406-8.563-23.4-19.5-.06.66-.1 1.326-.1 2 0 11.874 9.4 21.5 23.5 21.5s23.5-9.626 23.5-21.5c0-.675-.039-1.341-.1-2-.994 10.937-10.1 19.5-23.4 19.5z"
          fill="#f2c100"
        ></path>
        <path
          fill="#fffacf"
          d="M18.5 6.554a6.5 1.001 0 1 0 13 0 6.5 1.001 0 1 0-13 0"
        ></path>
        <path
          stroke-miterlimit="10"
          fill="none"
          stroke="#45413c"
          stroke-width="1.25"
          d="M1.5 25.552a23.5 21.5 0 1 0 47 0 23.5 21.5 0 1 0-47 0"
        ></path>
        <path
          d="M19.25 30.279s2.875-4.025 5.75-4.025 5.75 4.025 5.75 4.025m-1.725-9.2a4.886 4.886 0 0 1 3.45-1.725 4.886 4.886 0 0 1 3.45 1.725m-21.85 0a4.886 4.886 0 0 1 3.45-1.725 4.886 4.886 0 0 1 3.45 1.725"
          fill="none"
          stroke="#45413c"
          stroke-width="1.25"
          stroke-linecap="round"
          stroke-linejoin="round"
        ></path>
        <path
          d="M2.463 15.4a5.517 5.517 0 0 0 5.7 5.327 5.517 5.517 0 0 0 5.534-5.5c-.07-4.639-5-12.3-5.8-12.286S2.393 10.765 2.463 15.4z"
          fill="#00b8f0"
        ></path>
        <path
          d="M8.005 10.436a5.515 5.515 0 0 0-5.511 5.232c-.006-.09-.03-.173-.031-.264-.07-4.639 4.626-12.444 5.428-12.456s5.733 7.647 5.8 12.286c0 .091-.02.175-.023.265a5.515 5.515 0 0 0-5.663-5.063z"
          fill="#4acfff"
        ></path>
        <path
          d="M2.463 15.4a5.517 5.517 0 0 0 5.7 5.327 5.517 5.517 0 0 0 5.534-5.5c-.07-4.639-5-12.3-5.8-12.286S2.393 10.765 2.463 15.4z"
          fill="none"
          stroke="#45413c"
          stroke-width="1.25"
          stroke-linecap="round"
          stroke-linejoin="round"
        ></path>
      </svg>
    </label>
    <my-button :handleButton="closeDialog" class="form__button">
      Отменить
    </my-button>
    <my-button class="form__button" :isSubmit="true"> Отправить </my-button>
  </form>
</template>

<script>
export default {
  props: {
    parentCommentId: {
      type: Number,
      defualt: null,
    },
    closeDialog: Function,
    sendForm: Function,
  },
  data() {
    return {
      formData: {
        author: "",
        text: "",
        reaction: 0,
        parentId: null,
      },
    };
  },
  methods: {
    createComment() {
      this.formData = {
        author: this.formData.author,
        text: this.formData.text,
        reaction: +this.formData.reaction,
        parentId: this.parentCommentId,
      };
      // this.$emit('create', this.formData);
      this.sendForm(this.formData);
      this.formData = {
        author: "",
        text: "",
        reaction: 0,
        parentId: null,
      };
    },
  },
};
</script>

<style scoped lang="scss">
@use "@/assets/scss/function" as *;
@use "@/assets/scss/variables" as *;
@use "@/assets/scss/mixin" as *;
.form {
  display: flex;
  flex-direction: column;
}

.form__label {
  margin-top: 15px;
}
.form__text {
  font-size: 1.4rem;
  font-weight: 600;
}
.form__text + .form__input {
  margin-top: 7px;
}
.form__radio + .form__text {
  font-size: 2rem;
}
.form__img {
  width: 2rem;
}
.form__radio:checked + .form__img {
  border-bottom: 2px solid color(primaryTitleColor);
  opacity: 1;
  transition: all 0.3s linear;
}
.form__radio + .form__img {
  opacity: 0.5;
}
.form__button {
  margin-top: 15px;
  align-self: flex-end;
}
</style>
