<template>
  <v-list-group
    :group="item.to"
    :prepend-icon="item.icon"
    no-action
    v-bind="$attrs"
  >
    <template v-slot:activator>
      <v-list-item-content>
        <v-list-item-title
          v-if="item.title"
          v-text="item.title"
        />
      </v-list-item-content>
    </template>

    <template v-for="(child, i) in item.items">
      <documentation-list-sub-group
        v-if="child.items"
        :key="`sub-group-${i}`"
        :item="child"
      />

      <documentation-list-item
        v-else
        :key="`child-${i}`"
        :item="child"
      />
    </template>
  </v-list-group>
</template>

<script>
  export default {
    name: 'DocumentationListGroup',

    components: {
      DocumentationListItem: () => import('./ListItem'),
      DocumentationListSubGroup: () => import('./ListSubGroup'),
    },

    props: {
      item: {
        type: Object,
        default: () => ({}),
      },
    },
  }
</script>
