<template>  
  <v-list v-resize="setContainerWidth" class="tag-list" :class="`tag-list--${$props.align}`" ref="listContainer">
      <template v-for="(item, index) in listItems" >
        <v-list-item class="tag-list__el" v-if="shouldRenderItem(index)" :ref="setItemRef" :data-index="index" :key="index">
          <v-icon v-if="item.icon">
            {{item.icon}}
          </v-icon>
          {{ item.text }}
        </v-list-item>
        <v-icon class="tag-list__sep" ref="sepr"
            v-if="index < $props.dataTags.length - 1 && shouldRenderItem(index+1)"
            :key="`${index}-divider`"
        >mdi-circle-small</v-icon>
      </template>
  </v-list>
</template>

<script>
  export default {
    name: 'tagList',
    props: [
      'dataTags',
      'align'
    ],
    data: () => ({ 
      listWidth: 0,
      listItems: [],
      containerWidth: 0,
      itemWidths: []
    }),  
    created() {
      this.listItems = [...this.dataTags];
    },  
    mounted() {
      this.$nextTick(() => {
        this.setContainerWidth()
        this.calculateItemWidths();
      });
    },
    methods: {
      setContainerWidth(){
        if (this.$refs.listContainer) {
          this.containerWidth = this.$refs.listContainer.$el.clientWidth;
        }
      },
      setItemRef(el) {
        if (el) {
          this.$refs[el.$attrs['data-index']] = el;
        }
      },
      calculateItemWidths() {
        this.itemWidths = this.listItems.map((_, index) => {
          return this.$refs[index].$el.clientWidth + 24;
        });
      },
      shouldRenderItem(index) {
        let totalWidth = 0;
        for (let i = 0; i <= index; i++) {
          totalWidth += this.itemWidths[i] || 0;
          if (totalWidth > this.containerWidth) {
            return false;
          }
        }
        return true;
      }
    }
  }
</script>