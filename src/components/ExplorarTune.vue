<template style="padding-right: 0; margin-left: 0;margin-bottom: 0;margin-right: 0;margin-top: 0">

  <v-container color="black" flat style="padding-right: 0; margin-left: 0;margin-bottom: 0;margin-right: 0;margin-top: 0" fluid>


    <v-card class="mx-auto" max-width="50%" style="margin-bottom: 20px">

      <div style="height: auto">

        <br>
        <v-card-title style="padding: 0" class="pl-2" contain>
          <div>Explorar Artistas y Bandas Cercanas  Ver todo</div>
        </v-card-title>
        <v-card-text style="font-size:0.8em; padding:0" class="pl-2" contain>

          <ul style="list-style: none;">
            <v-row>
            <li v-for="category in 8" v-bind:key="category">
              <v-col cols="1">
                <v-btn>{{categories[category-1]}}</v-btn>
              </v-col>
            </li>
          </v-row>
            <v-row>
              <li v-for="category in 8" v-bind:key="category">
                <v-col cols="1">
                  <v-btn>{{categories[category-1+8]}}</v-btn>
                </v-col>
              </li>
            </v-row>
          </ul>

        </v-card-text>

      </div>

    </v-card>

    <v-card class="mx-auto" max-width="50%" style="margin-top: auto">

      <div style="height: auto">

        <br>
        <v-card-title style="padding: 0" class="pl-2" contain>
          <div>Explorar Institutos y Bares Cercanos  Ver todo <br></div>
        </v-card-title>
        <v-card-text style="font-size:0.8em; padding:0" class="pl-2" contain>

          <v-img src="../assets/staticmap.png"></v-img>



          <v-list three-line>
            <template v-for="(item, index) in items">
              <v-subheader
                  v-if="item.header"
                  :key="item.header"
                  v-text="item.header"
              ></v-subheader>

              <v-divider
                  v-else-if="item.divider"
                  :key="index"
                  :inset="item.inset"
              ></v-divider>

              <v-list-item
                  v-else
                  :key="item.title"
              >
                <v-list-item-icon>
                  <v-img src="../assets/club.png"></v-img>
                </v-list-item-icon>

                <v-list-item-content>
                  <v-row>
                    <v-col cols="2">
                  <v-list-item-title ><h3>{{item.title}}</h3></v-list-item-title>
                  <v-list-item-subtitle>{{item.distance}} km</v-list-item-subtitle>
                    </v-col>
                    <v-spacer></v-spacer>
                    <v-col cols="4">
                      <v-list-item-title ><h4><v-icon color="black">mdi-map-marker</v-icon>{{item.direction}}</h4></v-list-item-title>
                    </v-col>
                    <v-spacer></v-spacer>
                    <v-col cols="2">
                      <v-list-item-title ><v-btn><v-icon>mdi-forum</v-icon>Contactar</v-btn></v-list-item-title>
                    </v-col>
                  </v-row>
                </v-list-item-content>
              </v-list-item>
            </template>
          </v-list>












        </v-card-text>

      </div>

    </v-card>
  </v-container>

</template>

<script>
import Routines from "@/store/RoutineStore";
export default {
  data() {
    return {
      toggled: false,
      routines: Routines.get(),
      categories: ['Clasica','Rock','Pop','Metal','Jazz','Cumbia','Trap','Hip Hop','EDM','Tango','New Age','Funk','Punk','Rap','Elevator','Noise'],
      items: [
        { header: 'Establecimientos' },
        {
          avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
          title: 'Jactans',
          distance: 1.5,
          direction: ' Ciudad Autónoma de Buenos\n' +
              ' Aires, AR'
          },
        { divider: true, inset: true },
        {
          avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
          title: 'MJ Pub',
          distance: 2.3,
          direction: ' Ramos Mejía, AR'
        },
        { divider: true, inset: true },
        {
          avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg',
          title: 'Antidomingo',
          distance: 5,
          direction: ' Buenos Aires, AR'
        },
        { divider: true, inset: true },
        {
          avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
          title: 'Moly',
          distance: 6,
          direction: ' Buenos Aires, AR'
        },
        { divider: true, inset: true },
        {
          avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg',
          title: 'Club Araoz',
          distance: 6.66,
          direction: ' Buenos Aires, AR'
        },
      ],
    }
  },
}
</script>

<style scoped>
.bottom-right {
  position: absolute;
  bottom: 4px;
  right: 8px;
}
p {
  font-size: small;
  margin: 0;
}
span {
  display: block;
  color: white;
}
img.center {
  display: block;
  margin: 0 auto;
}
</style>
