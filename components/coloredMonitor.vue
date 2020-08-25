<template>
  <div class="container" :class="colorMapper[severity]">
    <div class="heading" v-if="hive != null && box == null">
      <span class="title">{{ hive }}</span>
    </div>
    <div class="heading" v-else>
      <span class="title">{{ hive || 'Becky' }}</span>
      <span class="subtitle">Box: {{ box || 'Brewed' }}</span>
    </div>

    <div class="reading">
      <i :class="'icon icon--' + typeMapper[type]"></i>
      <span class="value">{{ reading }}</span>
    </div>

    <div class="status">
      <label>Last reading:</label>
      <span class="value">{{ Math.floor(Math.random() * 10) }} minutes ago</span>

    <div class="indicator"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    severity: {
      type: String,
      required: false,
    },
    hive: {
      type: String,
      default: null
    },
    box: {
      type: String,
      default: null
    },
    type: {
      type: String,
      required: true
    },
    reading: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      colorMapper: {
        'ok': 'green',
        'warning': 'orange',
        'error': 'red'
      },
      typeMapper: {
        'humidity': 'raindrop',
        'weight': 'barometer',
        'temperature': 'thermometer'
      }
    }
  }

}
</script>
<style lang="scss" scoped>

.green {
  --primary: #8ad721;
  --border: rgba(138, 215, 33, .4);
  --background: #f7fef2;
}

.orange {
  --primary: #e5ac59;
  --border: rgba(229, 172, 89, .4);
  --background: #fff4e6;
}

.red {
  --primary: #da1f1e;
  --border: rgba(218, 31, 30, .2);
  --background: #feedef;
}


.container {
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;

  position: relative;
  height: 100%;
  margin: 0.5rem;
  padding: 1rem;
  font-weight: 500;

  background-color: var(--background);
  border: 2px solid var(--border);
  border-radius: 6px;
  box-shadow: 2px 2px 10px rgba(0,0,0,.1);

  & > div:not(:first-of-type) {
    margin-top: 1rem;
  }
}

.indicator {
  position: absolute;
  top: 0.4rem;
  right: 0.4rem;
  background-color: var(--primary);
  width: 1rem;
  height: 1rem;
  border-radius: 50%;
}

.heading {
  display: flex;
  flex-direction: column;

  .title {
    font-size: 1.8rem;
  }
  .subtitle {
    color: rgba(0,0,0,.6);
  }
}

.reading {
  color: var(--primary);
  .icon {
    font-size: 2.4rem;
  }
  .value {
    font-size: 3rem; 
  }
}

.status {
  display: flex;
  flex-direction: column;

  .value {
    color: rgba(0,0,0,.7);
  }
}
</style>
