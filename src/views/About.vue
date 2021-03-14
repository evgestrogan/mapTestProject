<template>
  <svg class="graph-svg container-border"></svg>
</template>

<script>
import * as d3 from 'd3'

export default {
  data () {
    return {

    }
  },
  mounted () {
    let svg = d3.select('svg')
    let width = svg.style('width').slice(0, (parseInt(svg.style('width').length) - 2))
    let height = svg.style('height').slice(0, parseInt(svg.style('height').length) - 2)
    let g = svg.append('g')

    let nodes = [
      { name: 'Человек', status: 'danger' },
      { name: 'Машина', status: 'normal'},
      { name: 'Документ', status: 'danger' },

    ]

    let edges = [
      { source: 0, target: 1 },
      { source: 0, target: 2 },
    ]

    let colors = {
      danger: 'red',
      normal: 'blue',
    }

    let forceSimulation = d3.forceSimulation()
      .force('link', d3.forceLink())
      .force('center', d3.forceCenter())

    forceSimulation.nodes(nodes)
      .on('tick', ticked)

    forceSimulation.force('link')
      .links(edges)
      .distance(function (d) {
        return 100
      })

    forceSimulation.force('center')
      .x(width / 2)
      .y(height / 2)

    let links = g.append('g')
      .selectAll('line')
      .data(edges)
      .enter()
      .append('line')
      .attr('stroke', function () {
        return 'black'
      })

    let gs = g.selectAll('.circleText')
      .data(nodes)
      .enter()
      .append('g')
      .call(d3.drag()
        .on('start', started)
        .on('drag', dragged)
      )

    gs.append('circle')
      .attr('r', 15)
      .attr('fill', function (d) {
        return colors[d.status]
      })

    gs.append('text')
      .attr('x', -15)
      .attr('y', -25)
      .text(function (d) {
        return d.name
      })

    function ticked () {
      links
        .attr('x1', function (d) { return d.source.x })
        .attr('y1', function (d) { return d.source.y })
        .attr('x2', function (d) { return d.target.x })
        .attr('y2', function (d) { return d.target.y })
      gs
        .attr('transform', function (d) { return 'translate(' + d.x + ',' + d.y + ')' })
    }

    function started (d) {
        forceSimulation.alphaTarget(1)
    }

    function dragged (d) {
      d.fx = d3.event.x
      d.fy = d3.event.y
    }
  }
}
</script>

<style scoped>
.graph-svg{
  width: 100%;
  height: 100%;
  display: inline-block;
}
</style>