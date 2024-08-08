<script>
    import { scaleLinear, scaleBand, scaleSqrt } from "d3-scale";
    import { fade } from "svelte/transition";
    import { format } from "d3-format";
    import { extent } from "d3-array";
    import { each } from "svelte/internal";

    export let monthData;
    // console.log(todayData)
    // console.log(extent(todayData))

    // const hourFormat = format("02")
    const stepsFormat = format(",");

    let data = [];

    let width = 120;
    let height = 140;

    monthData.forEach((d, i) => {
        // console.log(data)
        data.push({ value: d, day: i + 1 });
    });

    console.log(data);

    const margin = {
        top: 10,
        right: 20,
        bottom: 40,
        left: 10,
    };

    // console.log(extent(data, (d) => d.value))
    // console.log(extent(data, (d) => d.value))

    // X Scale
    $: radiusScale = scaleSqrt().domain([3000, 30000]).range([0, 50]);

    let hovered;
</script>

<div class="figure-container">
    {#each data as d, i}
        <div class="circle-element">
            <svg {width} {height}>
                <!-- svelte-ignore a11y-mouse-events-have-key-events -->
                <g
                    transform="translate({margin.left}, {margin.top})"
                    on:mouseleave={() => (hovered = null)}
                    on:mouseover={() => (hovered = d)}
                    transition:fade={{duration:1000}}
                >
                    <circle
                        cx="50"
                        cy="50"
                        r={radiusScale(16500)}
                        fill="transparent"
                        stroke="#b3c3cc"
                    />

                    <circle
                        cx="50"
                        cy="50"
                        r={radiusScale(30000)}
                        fill="transparent"
                        stroke="#b3c3cc"
                    />

                    <circle
                        cx="50"
                        cy="50"
                        r={radiusScale(d.value)}
                        out:fade={{ duration: 400 }} in:fade={{ delay: 400, duration: 400 }}
                        fill={hovered
                            ? hovered === d
                                ? "#ff6719"
                                : "#32444d"
                            : "#32444d"}
                    />

                    <text class="circle-text" x={(width - 20) / 2} y={margin.top + 110}
                    transition:fade={{ duration: 1000, delay:300}}>
                        {hovered ? (hovered === d ? stepsFormat(d.value) : d.day) : d.day}
                    </text>
                </g>
            </svg>
        </div>
    {/each}
</div>

<style>
    .figure-container {
        display: flex;
        flex-wrap: wrap;
    }

    .circle-text {
        text-align: center;
        text-anchor: middle;
    }
</style>
