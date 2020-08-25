<template>
  <div class="flex">
    <colored-monitor v-for="hive in hives" v-bind="hive" />
  </div>
</template>

<script>
import ColoredMonitor from 'components/coloredMonitor'

export default {
  components: { ColoredMonitor },
  data() {
    return {
      hives: [],
      names: ['Lisa', 'Jeniffer', 'Becky', 'Margaret', 'Betty', 'Hellen', 'Dorothy', 'Deborah', 'Michelle'],
      boxTypes: ['Brewed', 'Honey', 'Flow'],
      sensorTypes: ['humidity', 'temperature', 'weight'],
      severityLvls: ['ok', 'warning', 'error']
    }
  },
  methods: {
    randomFromList(list) {
      return list[Math.floor(Math.random() * list.length)];
    },
    randomReading(type) {
      if (type == 'humidity') {
        const value = Math.floor(Math.random() * (100-70) + 70);
        return `${value}%`
      }  else if (type == 'temperature') {
        const value = Math.floor(Math.random() * (35-28) + 28);
        return `${value}°`
      } else if (type == 'weight') {
        const val =  Math.floor(Math.random() * (60-20) + 20);
        return `${val}kg` 
      } else {
          return 'NaN'
      }
    },
    randomSeverity() {
      let chance = []
      chance = chance.concat(new Array(4).fill(this.severityLvls[0]));
      chance = chance.concat(new Array(2).fill(this.severityLvls[1]));
      chance = chance.concat(new Array(1).fill(this.severityLvls[2]));
      return this.randomFromList(chance)
    },
    getHiveData() {
      let data = [];
      const length = 5;
      for (let i = 0; i < length; i++) {
        let hive = this.randomFromList(this.names);
        let box = this.randomFromList(this.boxTypes);
        let type = this.randomFromList(this.sensorTypes);
        let reading = this.randomReading(type);
        let severity = this.randomSeverity();
        console.log(severity)
        data.push({ hive, box, type, reading, severity })
      }
      return Promise.resolve(data);
    }
  },
  beforeMount() {
    this.getHiveData()
      .then(data => this.hives = data)
  }
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
.name {
  color: pink;
}
</style>
