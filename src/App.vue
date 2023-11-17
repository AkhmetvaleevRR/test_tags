<template>
  <v-app> 
    <v-main>
      <!-- компонент на всю ширину экрана с выравниванием по левому краю -->
      <!-- <div class="container left">
        <tagList  
          :dataTags = tags
          :align = "'left'"
        />
      </div> -->
      <!-- компонент на всю ширину экрана с выравниванием по ширине, -->
      <div class="container wide">
        <tagList 
          :dataTags = tags
          :align = "'wide'"
        />
      </div>
      <div class="container">
        <!-- компонент на 50% ширины экрана с выравниванием по левому краю, -->       
        <div class="container__item half-left">      
          <tagList 
            :dataTags = tags
            :align = "'left'"
          />
        </div>
        <!-- компонент на 50% ширины экрана с выравниванием по ширине (можно на одной строке с предыдущим) -->
        <div class="container__item half-wide right">
          <tagList 
            :dataTags = tags
            :align = "'wide'"
          />   
        </div>
      </div>
    </v-main>
  </v-app>
</template>


<script>
import TagList from "./components/TagList";
import "./assets/tags.scss"

export default {
  name: "App",

  components: {
    TagList,
  },

  data: () => ({
    tags: [
      {
        text: "текст 1",
      },
      {
        text: "текст 2",
        icon: "mdi-check-circle",
      },
      {
        text: "текст 3",
        icon: "mdi-check-circle",
      },
    ],
  }),
};
</script>
