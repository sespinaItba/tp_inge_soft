<template>
  <div>
    <v-row>
      <v-app-bar width="100%" height="80%" color="black" app>
        <v-row>
          <v-spacer></v-spacer>
          <v-col cols="1">
            <v-btn icon router :to="home_link">
              <v-img max-width="35%" contain src="../../assets/favicon.png"/>
            </v-btn>
          </v-col>
          <v-spacer></v-spacer>

          <v-spacer></v-spacer>
          <v-col cols="1">
            <v-btn text style="alignment: center;color: white" router :to="home_link">Home</v-btn>
          </v-col>
          <v-col cols="1">
            <v-menu
                bottom
                min-width="200px"
                rounded
                offset-y>
              <template v-slot:activator="{ on }">
                <v-btn v-on="on" left text style="alignment: center;color: white">Explorar</v-btn>
              </template>
              <v-card>
                <v-list-item-content class="justify-center">
                  <div class="mx-auto text-center">
                    <v-btn router on to="/ExplorarArtistas"
                           depressed
                           rounded
                           text
                    >
                      Ver Artistas
                    </v-btn>
                    <v-divider class="my-3"></v-divider>
                    <v-btn router on to="/ExplorarInstitutos"
                           depressed
                           rounded
                           text
                    >
                      Ver Lugares
                    </v-btn>
                  </div>
                </v-list-item-content>
              </v-card>
            </v-menu>
          </v-col>
          <v-col cols="1">
            <v-btn text style="alignment: center;color: white" router :to="network_link">Network</v-btn>
          </v-col>
          <v-col cols="1">
            <v-btn text style="alignment: bottom;color: white" router @click="messageBtn">Mensajes</v-btn>
          </v-col>
          <v-col cols="1">
            <v-menu
                bottom
                min-width="200px"
                rounded
                offset-y>
              <template v-slot:activator="{ on }">
                <v-btn
                    icon
                    x-large
                    v-on="on"
                >
                  <v-avatar
                  >
                    <v-icon color="white">
                      mdi-account
                    </v-icon>
                  </v-avatar>
                </v-btn>
              </template>
              <v-card>
                <v-list-item-content class="justify-center">
                  <div class="mx-auto text-center">
                    <v-btn router on to="/Perfil"
                        depressed
                        rounded
                        text
                    >
                      Ver Perfil
                    </v-btn>
                    <v-divider class="my-3"></v-divider>
                    <v-btn @click="closeSession()"
                        depressed
                        rounded
                        text
                    >
                      Cerrar Sesion
                    </v-btn>
                  </div>
                </v-list-item-content>
              </v-card>
            </v-menu>
          </v-col>
        </v-row>
      </v-app-bar>
    </v-row>

  </div>
</template>

<script>
import {auth, db} from "@/db";

export default {
  data() {
    return {
      image: '',
      home_link: '/Home',
      explorar_link: '/Explorar',
      network_link: '/Network',
      mensajes_link: '/Mensajes',
      perfil_link: '/Perfil',
      loggedIn: true,
      user: {
        initials: 'GD',
        fullName: 'Gaston Donikian',
        email: 'gdonikian@itba.edu.ar'
      },
      onProfileScreen: false,
    }
  },
  async beforeMount() {
    await db.collection('users').doc( auth.currentUser.uid ).get().then( (elem) =>{
      const data = elem.data();
      this.image = data.profilePic;
    })
  },
  methods: {

    async messageBtn(){
      await this.$router.push({path: this.mensajes_link, query:{uid: null}});
    },
    closeSession() {
      auth.signOut().then(async ()=>{
        await this.$router.push('/');
      });
    },
    async deleteAccount(){
      console.log(auth.currentUser.uid)
      let posts = await db.collection("posts").where("uid", "==", auth.currentUser.uid).get()
        posts.docs.forEach( e=>{
          const data = e.data()
           db.collection("posts").doc(data.pid).delete()
        })
    }
  }
}
</script>

<style scoped>
#inProfile {
  color: white;
  background: orange;
}

{
  color: white
;
}

</style>
