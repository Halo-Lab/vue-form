<template>
  <form
    :class="['form', { [className]: className }]"
    @submit.prevent="() => onSubmit(submitHandler)"
    novalidate
  >
      <slot />
  </form>
</template>

<script>
import { provide } from 'vue';
import { useForm } from '@/hooks/useForm';

export default {
  props: {
    postUrl: {
      type: String,
      default: '',
    },
    className: {
      type: String,
      default: '',
    },
    submitHandler: {
      type: Function,
      default: null,
    },
  },
  setup(props) {
    const { postUrl } = props;
    const {
      registerField,
      onSubmit,
      hasFormErrors,
      getFieldError,
      setFieldError,
    } = useForm(postUrl);
    provide('registerField', registerField);
    provide('getFieldError', getFieldError);
    provide('hasFormErrors', hasFormErrors);
    provide('setFieldError', setFieldError);

    return { onSubmit };
  },
};
</script>

<style lang="scss">
@import './../assets/styles/style.scss';
</style>
