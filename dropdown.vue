Some other component

<template>
  <dropdown :open="dropdown_open" ref="dropdown">
    <template slot="button">
      <div v-if="bookmaked">
        Bookmarked
      </div>
      <div v-else>
        Bookmark
      </div>
    <template>
    <dropdown-item v-if="bookmarked" @click="removeFromBookmarks" :icon="times">
        Remove from bookmarks
    </dropdown-item>
  </dropdown>
</template>

<script>
import Dropdown from '~/components/Dropdown'
import DropdownItem from '~/components/DropdownItem'
export default {
  components: {
    { Dropdown, DropdownItem }
  },
  data: {
    selected: undefined,
    categories: [
      { name: 'Foo', value: 'foo' },
      { name: 'Bar', value: 'bar' },
    ]
  },
  methods: {
    removeFromBookmarks() {
      this.$refs.dropdown.close()
    }
  }
}
</script>




Dropdown

<template>
  <div>
    <button @click="local_open = !local_open">
      <slot name="button" />
    </button>
    <div class='dropdown-content' :class="{ 'open': local_open }">
      <slot>
        <dropdown-item v-for="items in items" @click="$emit('selected', item)" :item="item" :item_label="item_label" />
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      required: false,
    },
    item_label: {
      default: 'label'
    },
    items: {
      type: Array,
      required: false
    },
    prop_open: {
      default: false,
      type: Boolean
    }
  },
  data: {
    local_open: false
  },
  methods: {
    close() {
      this.local_open = false
    }
  }
}
</script>


Dropdown-item

<template>
  <div>
    <template v-if="seperator">
      <hr />
    </template>
    <template v-else>
      <a @click="$emit('click', item)">
        <icon :icon="icon" v-if="icon" /> 
        <slot>
          {{ label }}
        </slot>
      </a>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      required: false
    },
    item_label: {
      default: 'label'
    },
    icon: {
      required: false,
      type: string
    },
    separator: {
      default: false
    }
  },
  computed: {
    label() {
      return this.item[this.item_label]
    }
  }
}
</script>