<template>
  <div id="map" class="w-full h-screen" />
</template>

<script setup lang="ts">
import geoJson from '@/assets/gba.json'; // 大湾区 GeoJSON地图
import * as echarts from 'echarts';
import type { GeoJSONSourceInput } from 'echarts/types/src/coord/geo/geoTypes.js';
import { onMounted } from 'vue';

onMounted(() => {
  const chart = echarts.init(document.getElementById('map'));

  echarts.registerMap('GBA', geoJson as GeoJSONSourceInput);

  const option = {
    geo: {
      map: 'GBA',
      roam: true,
      label: { show: true },
      itemStyle: {
        normal: {
          areaColor: '#0f2c70',
          borderColor: '#1fffde',
        },
      },
    },
    series: [
      {
        type: 'lines',
        coordinateSystem: 'geo',
        zlevel: 2,
        effect: {
          show: true,
          constantSpeed: 40,
          symbol: 'arrow',
          symbolSize: 6,
          trailLength: 0.1,
        },
        lineStyle: {
          color: '#ffa022',
          width: 2,
          opacity: 0.6,
          curveness: 0.2,
        },
        data: [
          {
            coords: [
              [113.2644, 23.1291], // 广州
              [114.0579, 22.5431], // 深圳
            ],
          },
          {
            coords: [
              [113.2644, 23.1291],
              [113.5439, 22.2041], // 珠海
            ],
          },
        ],
      },
      {
        type: 'effectScatter',
        coordinateSystem: 'geo',
        zlevel: 2,
        rippleEffect: { brushType: 'stroke' },
        symbolSize: 10,
        itemStyle: { color: '#f4e925' },
        data: [
          { name: '广州', value: [113.2644, 23.1291] },
          { name: '深圳', value: [114.0579, 22.5431] },
          { name: '珠海', value: [113.5439, 22.2041] },
        ],
      },
    ],
  };

  chart.setOption(option);
});
</script>
