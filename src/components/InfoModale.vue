<template>
  <div class="text-center">
    <!--Boutons pour différentes parties du corps-->
    <v-btn
      v-for="part in bodyParts"
      :key="part.name"
      @click="openModal(part)"
      prepend-icon="mdi-checkbox-marked-circle"
      class="mb-4 mx-4"
    >
      {{ part.name }}
    </v-btn>

    <v-dialog v-model="dialog" width="auto">
      <v-card min-width="400" max-width="600">
        <v-card-title class="px-4 py-4">
          Explications
        </v-card-title>
        <v-card-text>
          <v-row>
            <v-col class="d-flex flex-column justify-center">
              <div class="text-with-arrow">
                <span class="left-text">{{ selectedPart.name }}</span>
                <span class="arrow">→</span>
                <span class="right-text">{{ selectedPart.dans_la_mer }}</span>
              </div>
              <div class="additional-text">
                {{ selectedPart.commentaire }}
              </div>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-btn class="ms-auto" text @click="dialog = false">Ok</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
  setup() {
    // Liste des parties du corps 
    const bodyParts = [
      {name: "Tête", dans_la_mer: "Réchauffement climatique", commentaire: "Les changements affectant le régime des courants et des vents peuvent provoquer des dérèglements climatiques comme des tempêtes violentes."},
      {name: "Estomac", dans_la_mer: "Biodiversité", commentaire: "Comme l’estomac où atterrit tout ce que nous ingérons, l’océan est le destinataire final de la plupart des déchets produits par les humains, car lui n’a pas d’intestins pour récolter les nutriments et évacuer le reste. La pollution marine résulte de tous les produits rejetés dans les mers et les océans en conséquence de l’activité humaine. Cette pollution arrive dans le milieu marin par le vecteur des voies fluviales, des vents, de l’air en basse latitude ou est directement rejetée à la mer."},
      {name: "Reins", dans_la_mer: "Estuaires", commentaire: "Des estimations indiquent que depuis le début des années 1950, plus de 8,3 milliards de tonnes de plastiques ont été produites, dont une grande partie se retrouve dans l’environnement, transportée par les fleuves. Les microparticules de plastique se retrouvent en quantité importante dans les océans et ont la capacité d’accumuler les polluants. Ces déchets aquatiques ont un impact indirect sur l’Homme car, ingérés par les espèces marines que nous consommons, ils se retrouvent directement dans nos estomacs !"},
      {name: "Peau", dans_la_mer: "Mangroves, barrière naturelle", commentaire: "Commentaire de la peauOn estime à six millions de tonnes par an la quantité d’hydrocarbures introduite dans les océans par l’activité humaine, ce qui constitue une cause fondamentale de la pollution des océans. Les eaux usées domestiques et de ruissellement contiennent de nombreux polluants (biologiques, chimiques et minéraux) qui peuvent perturber les équilibres écologiques. Les eaux de ruissellement peuvent être particulièrement polluées par le lessivage des sols et des surfaces imperméabilisées (routes, parkings, toits, …), par la remise en suspension des ordures stockées dans les décharges… De même nature que les eaux domestiques, elles peuvent en plus contenir des métaux lourds et toxiques : plomb, zinc, hydrocarbures, mercure…"},
      {name: "Sang", dans_la_mer: "Courants", commentaire: "Lorsque les glaces terrestres et aux pôles fondent, les changements de température et de salinité des eaux se multiplient et affectent la densité des masses d’eau, ce qui pourrait ralentir la plongée des eaux froides vers les grands fonds. Les courants marins pourraient donc être modifiés."},
      {name: "Poumon", dans_la_mer: "Adification et photosynthèse", commentaire: "Les poumons nous permettent d’absorber l’oxygène et d’éliminer le CO2 essentiels à notre survie. Les océans sont considérés comme le poumon de la planète puisqu’ils réalisent l’opération inverse pour tous les organismes vivants, via le phytoplancton, produire une grande partie de l’oxygène que nous respirons et absorber les gaz à effet de serre, assainissant ainsi l’atmosphère."},
      {name: "Sexe", commentaire: "Commentaire de la bite"}
    ];

    // Variable réactive
    const dialog = ref(false);
    const selectedPart = ref ({name: "", dans_la_mer: "", commentaire: ""});

    // Ouvrir la modale en fonction de la partie sélectionnée
    const openModal = (part: {name: string, dans_la_mer: string, commentaire: string}) => {
      selectedPart.value = part;
      dialog.value = true;
    };

    return {
      bodyParts,
      dialog,
      selectedPart,
      openModal,
    };
  },
};
</script>

<style scoped>
  .text-with-arrow {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 0;
  } 

  .text-with-arrow .right-text {
    font-weight: bold;
  }

  .text-with-arrow .arrow {
    flex-shrink: 0;
    margin: 0 8px;
    font-size: 20px;
  }

  .additional-text {
    margin-top: 16px;
    font-size: 14px;
    color: gray;
  }
</style>