<template>
  <div class="label">
    <t-icon
      class="label__icon"
      :class="{
        'animate-spin':
          iconType === 'loading' || iconData?.iconTypeValue === 'loading',
      }"
      :style="{
        fill: !!color ? color : iconData?.iconColor || iconColor.color,
      }"
      :icon="!!iconType ? iconType : iconData?.iconTypeValue"
    />
    <span
      class="label__title"
      :style="{
        color: !!color ? color : iconData?.iconColor || iconColor.color,
      }"
      v-if="title"
      >{{ title }}</span
    >
  </div>
</template>

<script lang="ts">
import { computed, toRefs } from "@vue/reactivity";
import TIcon from "../Icon/TIcon.vue";
export default {
  components: { TIcon },
  props: {
    iconType: String,
    title: String,
    color: String,
  },
  setup(props) {
    const { iconType, title } = toRefs(props);

    return {
      iconData: computed(() => {
        if (title) {
          switch (title.value) {
            case "Running":
              return {
                iconTypeValue: "check-in-circle-classic",
                iconColor: "#69C297",
              };

            case "Pending":
              return {
                iconTypeValue: "time",
                iconColor: "#FFB200",
              };

            case "Succeeded":
              return {
                iconTypeValue: "check-in-circle-classic",
                iconColor: "#69C297",
              };
            case "Completed":
              return {
                iconTypeValue: "check-in-circle-classic",
                iconColor: "#69C297",
              };
            case "Failed":
              return {
                iconTypeValue: "error",
                iconColor: "#FF5C56",
              };
            case "Unknown":
              return {
                iconTypeValue: "unknown",
                iconColor: "#FF8B59",
              };
          }
        }
      }),

      iconColor: computed(() => {
        if (iconType) {
          switch (iconType.value) {
            case "check-in-circle-classic":
              return { color: "#69C297" };
            case "loading":
              return { color: "#FFB200" };
            case "time":
              return { color: "#7D7D85" };
            case "refresh":
              return { color: "#59A5FF" };
            default:
              return { color: "#7D7D85" };
          }
        }
      }),
    };
  },
};
</script>

<style scoped>
.label {
  @apply flex items-center;
}
.label__icon {
  @apply fill-current;
  width: 16px;
  height: 16px;
}
.label__title {
  @apply pl-1 text-xs;
}
</style>
