<template>      
  <li class="list-group-item" > 
    <i :class="'fa fa-pencil'" @click="cardDetails" aria-hidden="true"></i>
    {{element.name}} 
  </li> 
</template>

<script>

export default {
  name: "card",
  components: {
    
  },
  props: ['element'],
  data() {
    return {
    };
  },
  methods: {
    cardDetails: function() {
      this.element.name = this.element.name + ' BLAAAAAAAAAAAAAAAAAAAAAAAAA'
    }
  },
  computed: {

  },
  watch: {

  }
};
</script>

<style>
.table > tr > td {
  vertical-align: top !important;
}
.flip-list-move {
  transition: transform 0.5s;
}

.no-move {
  transition: transform 0s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.hidden {
  /* display: block */
}

.list-group {
  min-height: 42px;
  background-color: #efefef;
}

.list-group-item {
  cursor: move;
}

.list-group-item i {
  cursor: pointer;
}
</style>

