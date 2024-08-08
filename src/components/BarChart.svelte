<script>
    import { scaleLinear, scaleBand } from "d3-scale";
    import { fade } from "svelte/transition";
    import { format } from "d3-format";
    import { extent } from "d3-array"
    import { each } from "svelte/internal";

    
    export let todayData;
    // console.log(todayData)
    // console.log(extent(todayData))

    const hourFormat = format("02")
    const stepsFormat = format(",")

    let data = []

   todayData.forEach((d, i) => {
    // console.log(data)
    data.push({value: d, hour: hourFormat(i)})
   }) 

   console.log(data)

    const margin = {
        top: 40,
        right: 20,
        bottom: 40,
        left: 20,
    };

    // console.log(extent(data, (d) => d.value))

    // X Scale
    // const elemWidth = document.getElementById("GFG").offsetWidth;

    let width = 1200;
    $: innerWidth = width - (margin.left + margin.right);
    $: xScale = scaleBand()
    .domain(data.map((d) => d.hour))
    .range([0, innerWidth])
    .padding(0.2);


    // // Y Scale
    let height = 280;
    let innerHeight = height - (margin.top + margin.bottom);
    let yScale = scaleLinear().domain([0, 1800]).range([0, innerHeight]);

    

    let hovered;
</script>

<div class="figure-container" bind:clientWidth={width}>
<svg {width} {height}>
{#each data as d, i}
          <!-- svelte-ignore a11y-mouse-events-have-key-events -->
          <g
            class="bar-container"
            transform="translate({xScale(d.hour)}, {margin.top})"
            height="{innerHeight}px"
            on:mouseleave={() => (hovered = null)}
            on:mouseover={() => (hovered = d)}
          >

          <rect
          height={innerHeight}
          width={xScale.bandwidth()}
          y="0"
          x="0"
          fill="transparent"
        />

          <text
              class="value-text"
              x={xScale.bandwidth() / 2}
              y={innerHeight - yScale(d.value) - 6}
              fill={hovered
                ? hovered === d 
                    ? "#ff6719"
                    : "transparent"
                : "transparent"}
            >
              {@html stepsFormat(d.value)}
            </text>

            <rect
              height={yScale(d.value)}
              width={xScale.bandwidth()}
              y={innerHeight - yScale(d.value)}
              x="0"
              fade:transition={{duration:1000}}
              fill={hovered
                ? hovered === d 
                    ? "#ffaa80"
                    : "#ff6719"
                : "#ff6719"}
            />

            <text
              class="hour-text"
              x={xScale.bandwidth() / 2}
              y={innerHeight + 18}
              fill="#ff6719"
            >
              {@html d.hour}
            </text>
          </g>
        {/each}
      </svg>
      </div>

<style>
.hour-text, .value-text{
  text-align: center;
  text-anchor: middle;
}



</style>
