
<template>
  <v-app id="inspire">
    <v-navigation-drawer
            v-model="drawer"
            app
            right
    >
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-home</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>Transac rapide</v-list-item-title>
          </v-list-item-content>
        </v-list-item>


      </v-list>
    </v-navigation-drawer>

    <v-app-bar
            app
            color="cyan"
            dark
    >
      <v-spacer />

      <v-toolbar-title>Gères ton argent en ligne</v-toolbar-title>

      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
    </v-app-bar>
<div id="rp">
  <div v-show="facture">

    <v-content>
      <v-container
              class="fill-height"
              fluid
      >
        <v-row
                align="center"
                justify="center"
        >
          <v-col class="text-center">
            <v-tooltip left>


              <span>Source</span>
            </v-tooltip>

            <v-tooltip right>
              <template v-slot:activator="{ on }">

                <v-btn
                        @click="facture=!facture"
                        large
                        href=""
                        target="_blank"
                        v-on="on"
                        class="ma-3"
                        outlined color="indigo"

                >
                  <v-title class="">Vos transferts en ligne</v-title>
                </v-btn>

              </template>


              <span>Bienvenue</span>

            </v-tooltip>


          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </div>
  <div v-show="!facture">







    <div id="add" style="display: flex; justify-content: center; flex-direction: row; margin-top: 5%; text-align: center; margin-left: 20%;width: 50%; padding: 2%; background-color: rgba(144, 144, 144, 0.46); border-radius: 10px;">
<div class="test" style="justify-content: space-between; flex-direction: row">
      <header>
        <div class="header">
          <h1>{{ headerTitle }}</h1><br><hr><br>
          <transition name="fade">
            <div id="message" v-if="showMsg" :style="{backgroundColor: msgColor}">{{ msg }}</div>
          </transition>
        </div>
      </header>

      <section>

        <form class="transferForm">
          <div class="input-box">
            <label for="Account-1">De:     </label>
            <select v-model="gBal" @change="autoSelect(gBal)" style="border-color: blue; border: solid gray 1px;border-radius: 5px;margin-left: 10px;padding: 5px;background-color: rgba(255, 255, 255, 0.46);">
              <option value="0">Selectionner un compte<i class="fas fa-arrows-alt-v"></i></option>
              <option value="1">Livret jeune</option>
              <option value="2">Compte courant</option>
            </select>
          </div>
          <br>
          <div class="input-box">
            <label for="Account-2">A: </label>
            <select v-model="cBal" style="border-color: blue; border: solid gray 1px;border-radius: 5px;margin-left: 10px;padding: 5px;background-color: rgba(255, 255, 255, 0.46);">
              <option value="0" >Selectionner un compte</option>
              <option value="1" id="opt1">Compte courant</option>
              <option value="2" id="opt2">Livret jeune</option>
            </select>
          </div>
          <br>
          <div class="input-box" >
            <label for="transferAmount">Montant: €{{ transferAmount }}</label><br>
            <input type="text" v-model="transferAmount" style="border-color: blue; border: solid gray 1px;border-radius: 5px;margin-left: 10px;padding: 5px;background-color: rgba(255, 255, 255, 0.46);" />
          </div>
          <br>
          <div class="input-box">
            <v-btn @click.prevent="makeTransfer" style="background-color: cornflowerblue; /* Green */
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
" >Transferer</v-btn>
          </div>
          <br>
        </form>
      </section>

      <section :class="revealClass">
        <div class="accounts">
          <ul>
            <li style="list-style-type: none;">
              <p>
                <strong>Livret jeune</strong>
              </p>
              <p :class="balance1">{{ goBalance }} €</p>
            </li>
            <li style="list-style-type: none;">
              <p>
                <strong>Compte courant</strong>
              </p>
              <p :class="balance2">{{ classicBalance }} €</p>
            </li>
          </ul>
        </div>
      </section>
  <div id="app">
    <v-app id="inspire" style="background-color:rgba(144, 144, 144, 0);min-height: 50px;">
      <v-container>
        <v-row dense>
          <v-col
                  v-for="(item, i) in items"
                  :key="i"
                  cols="12"
          >
            <v-card
                    :color="item.color"
                    dark
            >
              <div class="d-flex flex-no-wrap justify-space-between">
                <div>
                  <v-card-title
                          class="headline"
                          v-text="item.title"
                  ></v-card-title>

                  <v-card-subtitle v-text="item.artist"></v-card-subtitle>
                </div>

                <v-avatar
                        class="ma-3"
                        size="125"
                        tile
                >
                  <v-img :src="item.src"></v-img>
                </v-avatar>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </div>
    </div>



  </div>
  </div>
</div>







    <v-footer
            color="cyan"
            app
    >
      <v-spacer />

      <span class="white--text">&copy; 2020</span>
    </v-footer>
  </v-app>
</template>
<script src="https://kit.fontawesome.com/401a3ba5be.js" crossorigin="anonymous"></script>
<script>
  export default {
    name: 'LayoutsDemosBaselineFlipped',
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      facture: true,
      headerTitle: 'Mes comptes',
      goBalance: '50',
      classicBalance: '200.00',
      gBal: 0,
      cBal: 0,
      transferAmount: 0,
      msg: '',
      showMsg: false,
      msgColor: '',
      revealClass: 'slide',
      balance1: '',
      balance2: '',
      items: [
        {
          color: '#1F7087',
          src: 'https://images.prismic.io/portail-lcl-web%2Fee171ca7-a302-41a8-b884-23504e75b856_hero-timeline-projet-immobilier-640x300-lcl.jpg?auto=compress,format&rect=322,0,318,300&w=330&h=311',
          title: 'Nouvelle offre étudiante',
          artist: 'Premier achat, revente pour acheter plus grand, investissement immobilier ? LCL vous accompagne étape par étape dans votre projet immobilier !',
        },
        {
          color: '#1F7087',
          src: 'https://images.prismic.io/portail-lcl-web%2F01915d8c-2839-41c6-b772-5f44cb03e89a_heroe_pret-taux-zero.jpg?auto=compress,format&rect=218,0,422,300&w=502&h=357',
          title: 'Logement : comment bénéficier du prêt à taux 0 ?',
          artist: 'Pour un premier investissement immobilier, le Prêt à Taux Zéro (PTZ) peut s’ajouter à un crédit immobilier classique. Pour 2020, le dispositif est reconduit dans les mêmes conditions, à une nuance près...  ',
        },
      ],

    }),
    watch: {
      transferAmount: function() {
        var goAmount = parseFloat(this.goBalance);
        var classicAmount = parseFloat(this.classicBalance);
        var transAmt = parseFloat(this.transferAmount);
        if(transAmt > goAmount && this.cBal == 1) {
          this.showMessage("Vous n'avez pas les fonds suffisants pour effectuer le transfert. Essayez avec un montant inférieur", 'red');
        }
        if(transAmt > classicAmount && this.cBal == 2) {
          this.showMessage('Vous n\'avez pas les fonds suffisants pour effectuer le transfert. Essayez avec un montant inférieur', 'red');
        }
      }
    },
    methods: {

      makeTransfer: function() {
        var num = 0;
        if(this.transferAmount != 0) {
          if(this.cBal == '1' && this.gBal == '1') {
            this.goBalance = this.addSum(this.goBalance, this.transferAmount, 'Retirer');
            this.classicBalance = this.addSum(this.classicBalance, this.transferAmount, 'Ajouter');
            num = 2;
          }
          if(this.cBal == '2' && this.gBal == '2') {
            this.goBalance = this.addSum(this.goBalance, this.transferAmount, 'Ajouter');
            this.classicBalance = this.addSum(this.classicBalance, this.transferAmount, 'Retirer');
            num = 1;
          }
          this.resetForm(num);
        } else {
          this.showMessage('Entrez un montant', 'red');
        }
      },

      addSum(bal, amt, mode) {
        var b = parseFloat(bal);
        var a = parseFloat(amt);
        var sum;
        if(mode == 'Retirer') {
          sum = (b - a).toFixed(2);
        }
        if(mode == 'Ajouter') {
          sum = (b + a).toFixed(2);
        }
        return sum;
      },

      resetForm: function(num) {
        this.cBal = 0;
        this.gBal = 0;
        this.transferAmount = 0;
        this.showMessage('Tansfert effectué', 'green')
        this['balance' + num] = 'transfer-ani'
        document.getElementById('opt1').disabled = false;
        document.getElementById('opt2').disabled = false;
      },

      showMessage(msg, color) {
        this.showMsg = true;
        this.msg = msg;
        this.msgColor = color;
        var vm = this;
        setTimeout(function() {
          vm.showMsg = false;
        }, 2000);
      },

      autoSelect(num) {
        var opt1 = document.getElementById('opt1');
        var opt2 = document.getElementById('opt2');
        this.cBal = num;
        if(num == 1 || opt1.disabled == false) {
          opt2.disabled = true;
          opt1.disabled = false;
        }
        if(num == 2 || opt2.disabled == false) {
          opt1.disabled = true;
          opt2.disabled = false;
        }
      }
    }
  }
</script>

