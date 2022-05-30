<template>
  <ul class="site-navigation-item-children">
    <SiteNavItem v-for="subitem in item.submenu" :key="subitem.id" :item="getUpdatedSubitem(subitem)" />
  </ul>
</template>

<script>

export default {
  name: 'SiteNavItemParent',
  components: {
    SiteNavItem: () => import('~/components/SiteNavItem/index.vue'),
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getUpdatedSubitem(subitem) {
      return { ...subitem, slug: `${this.item.slug}/${subitem.slug}` };
    },
  },
};
</script>

<style lang="scss" scoped>
.site-navigation-item-children {
  border-left: 1px solid #33300050;
  padding: 0;
  margin-left: calc(1rem + 10px);
}

</style>
