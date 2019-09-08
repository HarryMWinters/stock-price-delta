<template>
  <div id="app">
    <Nav />
    <MultiGraph v-bind:stocks="stocks" />
    <ControlPanel v-bind:stocks="stocks" v-bind:dates="dates" />
  </div>
</template>

<script>
import Nav from "./components/nav//Nav.vue";
import ControlPanel from "./components/control-panel/ControlPanel.vue";
import MultiGraph from "./components/mutli-graph/MultiGraph.vue";

export default {
  name: "app",
  components: {
    Nav,
    MultiGraph,
    ControlPanel
  },
  data() {
    return {
      stocks: [
        {
          symbol: "GOOG",
          initialSharePrice: "1098.00",
          finalSharePrice: "1111.25",
          priceArray: [
            1204.9301,
            1211.38,
            1181.41,
            1168.39,
            1188.1,
            1192.85,
            1171.02,
            1167.84,
            1168.89,
            1151.29,
            1189.53,
            1191.25,
            1182.6899,
            1198.45,
            1177.6,
            1167.26,
            1164.29,
            1197.27,
            1174.71,
            1188.01,
            1204.8,
            1173.99,
            1169.95,
            1152.32,
            1193.99,
            1209.01,
            1216.68,
            1225.14,
            1239.41,
            1250.41,
            1132.12,
            1137.81,
            1146.21,
            1138.07,
            1130.1,
            1146.33,
            1146.35,
            1153.58,
            1150.34,
            1144.9,
            1144.21,
            1140.48,
            1124.83,
            1116.35,
            1131.59,
            1121.58,
            1111.25,
            1097.95,
            1080.91,
            1076.01,
            1079.8,
            1086.35,
            1115.52,
            1121.88,
            1111.42,
            1102.33,
            1103.6,
            1092.5,
            1085.35,
            1088.77,
            1077.03,
            1078.72,
            1080.38,
            1066.04,
            1044.34,
            1042.22,
            1053.05,
            1036.23,
            1103.63,
            1117.95,
            1116.46,
            1134.15,
            1133.47,
            1140.77,
            1151.42,
            1149.63,
            1138.85,
            1162.3,
            1178.98,
            1164.21,
            1120.44,
            1132.03,
            1164.27,
            1162.38,
            1166.27,
            1174.1,
            1189.39,
            1185.4,
            1162.61,
            1168.08,
            1188.48,
            1287.58,
            1272.18,
            1263.45,
            1256,
            1264.55,
            1248.84,
            1236.37,
            1236.34,
            1227.13
          ]
        }
      ],
      dates: {
        initial: "2019-07-01",
        final: "2019-07-02"
      }
    };
  }
};
</script>

<style>
* {
  --black: #020202;
  --eggshell: #ffffff;
  --lime: #8edce6;
  --grey: #454545;
  --forest: #4f9d69;

  --bg-element: #ffffff;
  --border: #45454538;

  margin: 0;
  padding: 0;
}

body {
  height: 100%;
  background: var(--eggshell);
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
