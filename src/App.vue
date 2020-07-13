<template>
  <div id="app">
    <NodeBox v-for="node in flowChartList" :node="node" :key="node.id"></NodeBox>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import NodeBox from './components/NodeBox.vue';
import TestData from './TestData.json';
@Component({
  components: {
    NodeBox,
  },
})
export default class App extends Vue {
  public flowChartData: any = TestData.data;

  get flowChartList() {
    const flowChartList: any[] = [];
    const startEventId = this.flowChartData.startEventId;
    const flowNodeMap = this.flowChartData.flowNodeMap;
    const startEventNode = {...flowNodeMap[startEventId]};

    flowChartList.push(startEventNode);

    function findNext(node: any, list: any[]) {
      if (!node.nextId || node.nextId === '99') { // 99 似乎是明道云流程结束的代码
        return;
      }

      if (flowNodeMap[node.nextId].typeId === 1) { // 分支节点
        const leftNode = flowNodeMap[flowNodeMap[node.nextId].flowIds[0]];
        const rightNode = flowNodeMap[flowNodeMap[node.nextId].flowIds[1]];
        const nextNode = {
          ...flowNodeMap[node.nextId],
          branchs: [],
        };

        for (const flowId of flowNodeMap[node.nextId].flowIds) {
          const flowNode = flowNodeMap[flowId];
          const flowList: any[] = [];

          nextNode.branchs.push(flowList);
          flowList.push(flowNode);
          findNext(flowNode, flowList);
        }

        list.push(nextNode);
        findNext(nextNode, list);
      } else {
        const nextNode = {...flowNodeMap[node.nextId]};
        list.push(nextNode);
        findNext(nextNode, list);
      }
    }
    findNext(startEventNode, flowChartList);
    return flowChartList;
  }
}
</script>

<style lang="less">
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

* {
  box-sizing: border-box;
}

body {
  background: rgb(245, 245, 249);
}
</style>
