<template>
  <v-container fill-height fluid class="background">
    <v-row>
      <v-col cols="12">
        <v-card class="pa-3" outlined width="600px">
          <v-card-title></v-card-title>
          <v-card-text>
            <v-form>
              <v-text-field
                v-model="ime"
                label="Ime"
                required
                :rules="[rules.required, rules.ruleIme]"
              ></v-text-field>
              <v-text-field
                v-model="prezime"
                label="Prezime"
                required
                :rules="[rules.required, rules.rulePrezime]"
              ></v-text-field>
              <v-text-field
                v-model="brojDolazaka"
                label="Broj dolazaka(maksimalno 15)"
                required
                :rules="[rules.required, rules.brDolazak]"
              ></v-text-field>
              <v-text-field
                v-model="prviKolokvij"
                label="Rezultat prvog kolokvija(maksimalno 40 bodova)"
                required
                :rules="[rules.required, rules.bodoviPrviKolokvij]"
              ></v-text-field>
              <v-text-field
                v-model="drugiKolokvij"
                label="Rezultat drugog kolokvija(maksimalno 40 bodova)"
                required
                :rules="[rules.required, rules.bodoviDrugiKolokvij]"
              ></v-text-field>
              <v-text-field
                v-model="kontinuiranoPracenje"
                label="Kontinuirano pracenje(maksimalno 20 bodova)"
                required
                :rules="[rules.required, rules.bodoviKontinuirano]"
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn
              color="black"
              class="white--text"
              elevation="0"
              @click="obrisiSveUnesenePodatke"
            >
              BRISI PODATKE
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn class="ocisti-button" @click="ocistiFormu">Očisti</v-btn>
            <v-btn
              class="OK-button"
              @click="ocistiFormu"
              :disabled="!isButtonDisabled"
              >OK</v-btn
            >
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
  
  <script>
export default {
  name: "prvi-zadatak",
  data() {
    return {
      ime: "",
      prezime: "",
      brojDolazaka: "",
      prviKolokvij: "",
      drugiKolokvij: "",
      kontinuiranoPracenje: "",
      rules: {
        required: (value) => !!value || "Required.",
        brDolazak: (v) => (v <= 15 && v > 0) || "Not valid",
        bodoviPrviKolokvij: (v) => (v <= 40 && v > 0) || "Not valid",
        bodoviDrugiKolokvij: (v) => (v <= 40 && v > 0) || "Not valid",
        bodoviKontinuirano: (v) => (v <= 20 && v > 0) || "Not valid",
      },
      isButtonDisabled: false,
    };
  },
  watch: {},
  methods: {
    ocistiFormu() {
      this.ime = null;
      this.prezime = null;
      this.brojDolazaka = null;
      this.prviKolokvij = null;
      this.drugiKolokvij = null;
      this.kontinuiranoPracenje = null;
    },
    dodajStudenta() {
      let noviStudent = {
        ime: this.ime,
        prezime: this.prezime,
        brojDolazaka: this.brojDolazaka,
        prviKolokvij: this.prviKolokvij,
        drugiKolokvij: this.drugiKolokvij,
        kontinuiranoPracenje: this.kontinuiranoPracenje,
      };
      //ovo ne diraj
      let studenti = JSON.parse(localStorage.getItem("studenti"));
      if (!studenti) {
        studenti = [];
      }
      studenti.push(noviStudent);
      localStorage.setItem("studenti", JSON.stringify(studenti));
    },
    obrisiSveUnesenePodatke() {
      localStorage.clear();
    },
  },
  computed: {
    isButtonDisabled() {
      return (
        !this.ime ||
        !this.prezime ||
        !this.brojDolazaka ||
        !this.prviKolokvij ||
        this.drugiKolokvij ||
        !this.kontinuiranoPracenje
      );
    },
  },
};
</script>
  
<style scoped>
.ocisti-button {
  color: red;
  border: solid 1px red;
}
</style>