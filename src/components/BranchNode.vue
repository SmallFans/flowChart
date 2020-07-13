<template>
  <div class="branch-node">
    <div class="branch" :class="{
      left: i === 0,
      right: i === node.branchs.length - 1
    }" v-for="(branch, i) in node.branchs" :key="i">
      <div class="line"></div>
      <div class="top-line"></div>
      <div class="bottom-line"></div>
      <NodeBox v-for="node in branch" :node="node" :key="node.id"></NodeBox>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import NodeBox from './NodeBox.vue';

@Component({
  components: {
    NodeBox: {},
  },
})
export default class BranchNode extends Vue {
  @Prop({ required: true }) public node!: any;

  private beforeCreate() {
    (this.$options.components as any).NodeBox = NodeBox;
  }
}
</script>

<style lang="less">
.branch-node {
  position: relative;
  display: flex;
  justify-content: center;
  background: rgb(245, 245, 249);
  z-index: 1;
}

.branch-node .branch {
  position: relative;
}

.branch-node .top-line,
.branch-node .bottom-line {
  position: absolute;
  margin: auto;
  width: 100%;
  height: 1px;
  background-color: #ccc;
  z-index: 0;
}

.branch-node .left .top-line,
.branch-node .left .bottom-line,
.branch-node .right .top-line,
.branch-node .right .bottom-line {
  width: 50%;
}

.branch-node .bottom-line {
  bottom: 0;
}

.branch-node .left .top-line,
.branch-node .left .bottom-line {
  right: 0;
}
</style>
