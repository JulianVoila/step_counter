<script>
  import { format } from "d3-format";

export let textContent;
export let value;

const stepsFormat = format(",.0f")

</script>

<div>
<h2>{textContent}</h2>
<p>{stepsFormat(value)} steps</p>
</div>

<style>
  h2 {
    color: #b3c3cc;
    margin-bottom: 0.1rem;
  }

  div{
    margin-bottom: 2rem;
  }

  p{
    font-size: 1.5rem;
    }
</style>