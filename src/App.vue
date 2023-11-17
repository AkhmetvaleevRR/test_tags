<template>
  <v-app> 
    <v-main>
      <!-- компонент на всю ширину экрана с выравниванием по левому краю -->
      <div class="container container--left">
        <tagList  
          :dataTags = tags
          :align = "'left'"
        />
      </div>
      <!-- компонент на всю ширину экрана с выравниванием по ширине, -->
      <div class="container container--width">
        <tagList 
          :dataTags = tags
          :align = "'width'"
        />
      </div>
      <div class="container">
        <!-- компонент на 50% ширины экрана с выравниванием по левому краю, -->       
        <div class="container__item container--half-left">      
          <tagList 
            :dataTags = tags
            :align = "'left'"
          />
        </div>
        <!-- компонент на 50% ширины экрана с выравниванием по ширине (можно на одной строке с предыдущим) -->
        <div class="container__item container--half-width">
          <tagList 
            :dataTags = tags
            :align = "'width'"
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
        icon: "mdi-thumb-up",
      },   
      {
        text: "текст 4",
        icon: "mdi-cloud-upload",
      },
    ],
  }),
};
</script>
