<template>
  <v-footer absolute color="transparent">
    <v-col class="text-right" cols="12">
      <v-dialog v-model="dialog" width="500">
        <template v-slot:activator="{ on, attrs }">
          <v-btn outlined color="white" class="px-8" v-bind="attrs" v-on="on"> Rules </v-btn>
        </template>

        <v-card>
          <v-card-title>
            <span class="text-h5 font-weight-bold">RULES</span>
            <v-spacer></v-spacer>
            <v-btn icon @click="dialog = false">
              <v-icon>mdi-close</v-icon>
            </v-btn>
          </v-card-title>

          <v-card-text class="px-6 pt-6 pb-12">
            <v-img :src="ruleImage"></v-img>
          </v-card-text>
        </v-card>
      </v-dialog>
    </v-col>
  </v-footer>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      ruleImage: require("../../../images/image-rules-bonus.svg"),
    };
  },
};
</script>
