<template>  
  <v-list class="tag-list" :class="`tag-list--${$props.align}`" ref="listContainer">
      <div v-for="(item, index) in listItems" :ref="setItemRef" :key="index">
        <div v-if="shouldRenderItem(index)" :key="index">
          <v-list-item class="tag-list__el" :key="index">
            <v-icon v-if="item.icon">
              {{item.icon}}
            </v-icon>
            {{ item.text }}
          </v-list-item>
          <v-icon class="tag-list__sep"
              v-if="index < $props.dataTags.length - 1"
              :key="`${index}-divider`"
          >mdi-circle-small</v-icon>        
        </div>
      </div>
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
      listContainer: [],
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
        if (this.$refs.container) {
          this.containerWidth = this.$refs.container.clientWidth;
          this.calculateItemWidths();
        }
      });
    },
    methods: {
      setItemRef(el) {
        if (el) {
          this.$refs[el.getAttribute('data-index')] = el;
        }
      },
      calculateItemWidths() {
        this.itemWidths = this.items.map((_, index) => {
          return this.$refs[index].clientWidth;
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
      // calcListWidth(){
      //   this.listContainer = document.querySelector('.tag-list'); //The list 
      //   this.listItems  = document.querySelectorAll('.tag-list__el, .tag-list__sep'); //The list items
      //   this.listWidth = 0
      //   for(let i = 0; i < this.listItems.length; i++) {
      //       this.listWidth += this.listItems[i].offsetWidth;            
      //     if(this.listWidth > this.listContainer.offsetWidth) { 
      //       console.log(this.listWidth + '>' + this.listContainer.offsetWidth)
      //       this.listItems[i].style.display = 'none';
      //     }         
      //   }
      // }
    }
  }
</script>

mounted() {
  
},
methods: {
  
  
  
}