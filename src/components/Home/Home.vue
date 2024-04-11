  <template>
      <div class="home">
        <Card  :search="search"/>
      </div>
    </template>
    
    <script setup>
    import Card from './Card.vue'

    //import { defineProps } from 'vue';
    const props=defineProps({

      search:{
        type:String,
        default:''
      }


    })
    console.log("Inside Home ",props.search);
    </script>
    
    <style scoped>
    .home {
      padding: 20px;
      margin-top: 70px;
    }
    </style>
    