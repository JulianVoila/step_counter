<script>
  import Example from "$components/Example.svelte";
  import TextCounter from "$components/TextCounter.svelte";
  import BarChart from "$components/BarChart.svelte";
  import CircleChart from "$components/CircleChart.svelte";
  import data from "$data/data.js";
    import { max, mean, min, sum } from "d3-array";

  let todayData = data[0].todayData
  let monthData = data[0].monthData


  // console.log(todayData);
  console.log(min(monthData));

  let divWidth = document.getElementById("CC")
  console.log(divWidth)
  let width = 1200;
</script>


<main class="main-container">
  <div class="left-container">
    <h2>Hello, Jules!</h2>
    <TextCounter textContent={"WORST DAY"} value={min(monthData)}></TextCounter>
    <TextCounter textContent={"AVG DAY"} value={mean(monthData)}></TextCounter>
    <TextCounter textContent={"BEST DAY"} value={max(monthData)}></TextCounter>
    <TextCounter textContent={"TOTAL LAST 28 DAYS"} value={sum(monthData)}></TextCounter>
    <TextCounter textContent={"TOTAL SO FAR TODAY"} value={sum(todayData)}></TextCounter>
    <TextCounter textContent={"WORST DAY"} value={max(monthData)-min(monthData)}></TextCounter>
  </div>
  <div class="right-container" id="CC">
    <div class="today-container">
      <h2>Today</h2>
      <div class="bar-container" >
        <BarChart todayData={todayData}></BarChart>
      </div>
    </div>
    <div class="month-container">
      <h2>Last 28 days</h2>
      <div class="circle-container">
        <CircleChart {monthData}></CircleChart>
      </div>
    </div>
  </div>
</main>

<style>

/* :root {
  --background-main: #edf4f7;
  --background-side: #f4f8fa;
  --primary-blue: #32444d;
  --secondary-blue: #b3c3cc;
  --primary-orange: #ff6719;
  --secondary-orange: #ffaa80;
} */

  main {
    min-height: 100vh;
    background: #edf4f7;
    display: flex;
  }

  .left-container {
    width: 20%;
    min-width: 250px;
    background-color: #f4f8fa;
    /* height: 100%; */
    min-height: 100vh;
    padding: 2rem;
  }

  .right-container {
    padding: 2rem;
  }

  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    font-weight: 700;
  }

  h2 {
    font-size: 1.5rem;
    color: #333;
    margin-bottom: 2rem;
    line-height: 1.5;
  }

  pre {
    padding: 1px 6px;
    display: inline;
    margin: 0;
    background: #ffb7a0;
    border-radius: 3px;
  }

  a {
    color: #ff3e00;
    text-decoration: inherit;
  }

  footer {
    font-size: 1rem;
    color: #333;
  }
</style>
