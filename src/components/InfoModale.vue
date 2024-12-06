<template>
  <div class="text-center">
    <v-btn
      v-for="part in bodyParts"
      :key="part.name"
      @click="openModal(part)"
      :id="part.name"
      prepend-icon="mdi-checkbox-marked-circle"
      class="mb-4 mx-4"
      style = "visibility: hidden"
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

          <!-- Afficher la vidéo si elle existe -->
          <v-row v-if="selectedPart.videoId" class="video-container">
            <v-col>
              <v-responsive>
                <iframe
                  :src="`https://www.youtube.com/embed/${selectedPart.videoId}`"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                  class="video-iframe"
                ></iframe>
              </v-responsive>
            </v-col>
          </v-row>

          <!-- Message si aucune vidéo n'est disponible -->
          <v-row v-else>
            <v-col class="text-center text-gray">
              <p>Aucune vidéo disponible pour cette partie.</p>
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
    const bodyParts = [
      {
        name: "Tête",
        dans_la_mer: "Réchauffement climatique",
        videoId: "-xc0LoOzuus",
        commentaire: "Lorsque les glaces terrestres et aux pôles fondent, les changements de température et de salinité des eaux se multiplient et affectent la densité des masses d’eau, ce qui pourrait ralentir la plongée des eaux froides vers les grands fonds. Les courants marins pourraient donc être modifiés.\n" +
          "Les changements affectant le régime des courants et des vents peuvent provoquer des dérèglements climatiques comme des tempêtes violentes.\n",
      },
      {
        name: "Sang",
        dans_la_mer: "Réchauffement climatique",
        videoId: "-xc0LoOzuus",
        commentaire: "Lorsque les glaces terrestres et aux pôles fondent, les changements de température et de salinité des eaux se multiplient et affectent la densité des masses d’eau, ce qui pourrait ralentir la plongée des eaux froides vers les grands fonds. Les courants marins pourraient donc être modifiés.\n" +
          "Les changements affectant le régime des courants et des vents peuvent provoquer des dérèglements climatiques comme des tempêtes violentes.\n",
      },
      {
        name: "Rein",
        dans_la_mer: "Estuaire",
        videoId: "bIpmzuuyASY",
        commentaire: "Lorsque les glaces terrestres et aux pôles fondent, les changements de température et de salinité des eaux se multiplient et affectent la densité des masses d’eau, ce qui pourrait ralentir la plongée des eaux froides vers les grands fonds. Les courants marins pourraient donc être modifiés.\n" +
          "Les changements affectant le régime des courants et des vents peuvent provoquer des dérèglements climatiques comme des tempêtes violentes.\n",
      },
      {
        name: "Peau",
        dans_la_mer: "Mangroves",
        videoId: "bIpmzuuyASY",
        commentaire: "La peau est la première ligne de défense de l'organisme contre les agressions extérieures (micro-organismes, produits chimiques, rayons UV...). Elle forme une barrière physique et immunitaire.\n" +
        "La peau et la mangrove, bien que distinctes, partagent cette fonction fondamentale de la protection. Toutes deux agissent comme des boucliers, protégeant ce qu elles entourent des agressions extérieures.\n" +
        "Les mangroves offrent une multitude de services écosystémiques essentiels à la vie sur Terre. Elles agissent comme une barrière contre l'érosion, les racines des palétuviers stabilisent les sédiments, réduisant ainsi l'érosion côtière due aux vagues et aux courants.\n" +
        "Elles filtrent également les sédiments, les nutriments et les polluants présents dans l'eau, améliorant ainsi sa qualité.\n" +
        "Les mangroves offrent également un habitat essentiel pour de nombreuses espèces marines, notamment les poissons, les crustacés et les mollusques, servant de nurserie pour leurs juvéniles. Elles abritent ainsi une biodiversité exceptionnelle, tant végétale qu'animale. Elles sont des écosystèmes complexes où de nombreuses espèces interagissent.\n"
      },
      {
        name: "Poumons",
        dans_la_mer: "CO2 / O2, acidification et photosynthèse",
        videoId: "44pp5k2ZFpE",
        commentaire: "Les poumons nous permettent d’absorber l’oxygène et d’éliminer le CO2 essentiels à notre survie. Les océans sont considérés comme le poumon de la planète puisqu’ils réalisent l’opération inverse pour tous les organismes vivants, via le phytoplancton : produire une grande partie de l’oxygène que nous respirons et absorber les gaz à effet de serre, assainissant ainsi l’atmosphère.\n" +
        "Le phytoplancton est capable, en utilisant l’énergie lumineuse du soleil et les sels nutritifs dissous dans l’eau de mer, de fixer de grandes quantités de dioxyde de carbone pour synthétiser les molécules permettant de fabriquer de nouvelles cellules. On estime que ces microorganismes sont responsables d’environ la moitié de la fixation de carbone sur Terre. Les cyanobactéries sont les seules bactéries capables de faire la photosynthèse oxygénique et elles sont d’ailleurs, évolutivement parlant, à l’origine de la photosynthèse des plantes terrestres.\n" +
        "Depuis la fin des années 1980, 95 % des eaux océaniques de surface en haute mer ont vu leur acidité augmenter. Les océans absorbent environ 30 % du dioxyde de carbone (CO2) que nous produisons, ce qui réduit le pH de l’eau de mer. C’est ce que l’on appelle l’acidification des océans. Avec des taux de CO2 dans l’air supérieurs de 50 % aux niveaux pré-industriels, le problème continue de s’aggraver.\n" +
        "Pour les écosystèmes marins, l’acidification des océans pose un double problème : une acidité plus élevée et une diminution des ions carbonates (CO32-). Les organismes calcifiants, comme les huîtres, les crabes, les oursins, les homards et les coraux, ont besoin de CO32- pour développer et entretenir leur coquille et leur squelette. Des études indiquent également que la coquille et le squelette de ces organismes se décomposent plus facilement lorsque l’acidité augmente.\n" +
        "En dépensant de l’énergie pour résister à des conditions plus acides, les organismes peuvent amenuiser les ressources dont ils disposent pour les processus physiologiques, tels que la reproduction et la croissance, ce qui peut menacer la stabilité des chaînes alimentaires, la résilience de l’écosystème et les activités économiques telles que la pêche et le tourisme.\n"

      },
      {
        name: "Estomac",
        dans_la_mer: "Biodiversité",
        videoId: "", // Pas de vidéo
        commentaire: "Comme l’estomac où atterrit tout ce que nous ingérons, l’océan est le destinataire final de la plupart des déchets produits par les humains, car lui n’a pas d’intestins pour récolter les nutriments et évacuer le reste.\n" +
          "La pollution marine résulte de tous les produits rejetés dans les mers et les océans en conséquence de l’activité humaine. Cette pollution arrive dans le milieu marin par le vecteur des voies fluviales, des vents, de l’air en basse latitude ou est directement rejetée à la mer.\n" +
          "Les déchets plastiques\n" +
          "Des estimations indiquent que depuis le début des années 1950, plus de 8,3 milliards de tonnes de plastiques ont été produites, dont une grande partie se retrouve dans l’environnement, transportée par les fleuves. Les microparticules de plastique se retrouvent en quantité importante dans les océans et ont la capacité d’accumuler les polluants. Ces déchets aquatiques ont un impact indirect sur l’Homme car, ingérés par les espèces marines que nous consommons, ils se retrouvent directement dans nos estomacs !\n" +
          "Le pétrole\n" +
          "On estime à six millions de tonnes par an la quantité d’hydrocarbures introduite dans les océans par l’activité humaine, ce qui constitue une cause fondamentale de la pollution des océans. Les eaux usées domestiques et de ruissellement contiennent de nombreux polluants (biologiques, chimiques et minéraux) qui peuvent perturber les équilibres écologiques. Les eaux de ruissellement peuvent être particulièrement polluées par le lessivage des sols et des surfaces imperméabilisées (routes, parkings, toits, …), par la remise en suspension des ordures stockées dans les décharges… De même nature que les eaux domestiques, elles peuvent en plus contenir des métaux lourds et toxiques : plomb, zinc, hydrocarbures, mercure…\n",
      },
    ];

    const dialog = ref(false);
    const selectedPart = ref({ name: "", dans_la_mer: "", videoId: "", commentaire: "" });

    const openModal = (part: { name: string; dans_la_mer: string; videoId: string; commentaire: string }) => {
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

.text-gray {
  color: gray;
}
</style>
