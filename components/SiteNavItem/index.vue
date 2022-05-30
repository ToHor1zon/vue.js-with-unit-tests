<template>
  <li
    class="site-navigation-item"
    :class="{
      'site-navigation-item--last-child': !isParent,
      'site-navigation-item--opened-parent': isParent && isOpenedNavItemParent,
      'site-navigation-item--closed-parent': isParent && !isOpenedNavItemParent,
    }"
    @click.stop="toggleNavItem"
  >
    <template v-if="isParent">
      <p
        class="site-navigation-item__name site-navigation-item__name--parent-title"
      >
        {{ item.name }}
        <span class="site-navigation-item__count">({{ item.product_count }})</span>
      </p>
      <SiteNavItemChildren v-if="isParent && isOpenedNavItemParent" :item="item" />
    </template>
    <nuxt-link v-else class="site-navigation-item__name" :to="item.slug">
      {{ item.name }}
      <span class="site-navigation-item__count">({{ item.product_count }})</span>
    </nuxt-link>
  </li>
</template>

<script>
import SiteNavItemChildren from '~/components/SiteNavItem/Children/index.vue';

export default {
  name: 'SiteNavItem',
  components: {
    SiteNavItemChildren,
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isOpenedNavItemParent: false,
    };
  },
  computed: {
    isParent() {
      return Boolean(this.item.submenu?.length);
    },
  },
  methods: {
    toggleNavItem() {
      this.isOpenedNavItemParent = !this.isOpenedNavItemParent;
    },
  },
};
</script>

<style lang="scss" scoped>
.site-navigation-item {
  display: block;
  width: 100%;
  height: 47px;
  position: relative;
  padding: 0.75rem 1rem;
  padding-left: calc(1rem + 10px);
  user-select: none;
  cursor: pointer;

  &--opened-parent {
    height: auto;
    padding: 0;

    & > .site-navigation-item__name {
      padding: 0.75em 0;
      padding-left: calc(1rem + 10px);
      font-weight: 700;
    }
  }

  &__name {
    color: #333;
  }

  &__name,
  &--last-child,
  &--closed-parent {
    &:hover,
    &:active {
      background-color: rgb(130, 0, 255);
      color: rgb(255, 255, 255);

      & > .site-navigation-item__name {
        color: rgb(255, 255, 255);
      }
    }
  }

  &__count {
    font-size: 14px;
    color: #c9cbca;
  }
}
</style>
