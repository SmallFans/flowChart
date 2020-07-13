<template>
  <div class="node-box">
    <branch-node v-if="node.typeId === 1" :node="node"></branch-node>
    <div v-else class="node">
      <div class="header">{{node.name}}</div>
      <div class="body">设置节点</div>
    </div>
    <div class="line"></div>
    <div class="btn">
      <i>+</i>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import BranchNode from './BranchNode.vue';

@Component({
  components: {BranchNode},
})
export default class NodeBox extends Vue {
  @Prop({ required: true }) public node!: any;
}
</script>

<style lang="less">
.node-box {
  position: relative;
  text-align: center;
  padding: 50px 50px 0px;
  z-index: 1;
}

.node-box .node {
  position: relative;
  width: 280px;
  background: #fff;
  border-radius: 6px;
  position: relative;
  box-shadow: 0 1px 4px rgba(0,0,0,.16);
  display: flex;
  flex-direction: column;
  cursor: pointer;
  display: inline-block;
  z-index: 1;
}

.node-box .header{
  width: 100%;
  height: 60px;
  position: relative;
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
  font-size: 15px;
  background: linear-gradient(rgba(0, 204, 102, 0.75) 0%, rgb(0, 204, 102) 100%);
  color: #fff;
  padding: 26px 10px 0;
  box-sizing: border-box;
}

.node-box .body {
  padding: 8px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 50px;
  color: #2196f3;
}

.node-box .btn {
  padding: 20px 0;
  width: 100%;
  position: relative;
  text-align: center;
}

.node-box .btn i {
  width: 21px;
  height: 21px;
  display: block;
  font-size: 20px;
  cursor: pointer;
  position: relative;
  background: #888888;
  color: #ccc;
  margin: 0 auto;
  font-style: normal;
  font-weight: 400;
  font-variant: normal;
  text-transform: none;
  line-height: 18px;
  border-radius: 50%;
  padding-left: 0px;
}
.node-box .line {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 1px;
  height: 100%;
  background-color: #ccc;
  z-index: 0;
}
.node-box:first-child .line {
  top: 100px;
}
</style>
