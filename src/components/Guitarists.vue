<template>
<div id="main">
  <h1 id="title">Famous Guitarists</h1>
  <add-guitarist
    :on-add="handleAdd"
  />
  <ul>
    <guitarist 
      v-for="guitar in guitarists"
      :key="guitar.name"
      :guitarist="guitar"
    />
  </ul>
</div>
</template>

<script>
import Guitarist from './Guitarist'
import AddGuitarist from './AddGuitarist'
import { getGuitarists, addGuitarist } from '../services/api';
export default {
  components: {
    Guitarist,
    AddGuitarist
  },
  data() {
    return {
      guitarists: null
    }
  },
  created() {
    getGuitarists()
      .then(guitarists => {
        this.guitarists = guitarists;
      });
  },
  methods: {
    handleAdd(guitarist) {
      return addGuitarist(guitarist)
        .then(data => {
          this.guitarists.push(data);
        });
    }
  }
}
</script>

<style>
#main {
  width: 100%;
  }

ul {
  margin: auto;
  width: 800px;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  justify-content: space-between; 
}

#title {
  font-size: 4rem;
  color: seashell;
  border-left: 1px solid black;
  border-right: 1px solid black;
  background: rgba(0, 0, 0, .69);
  margin: auto;
}
</style>
