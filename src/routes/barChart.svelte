<script>
    import { scaleBand, scaleLinear } from "d3-scale";
  
    export let data;
  
    let width = 300;
    let height = 200;
  
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };
    const innerHeight = height - margin.top - margin.bottom;
    const innerWidth = width - margin.left - margin.right;

    

    /*
    TODO
    - mapear todos os Medium dos items da Array (que é nosso d or data.picks)
    - Criar set para pegar valores unicos
    - OU simplesmente contar os valores
    - A array [] tem que conter valores para serem iterados por d3
    - Uma array com objetos onde os key são: medium e count
    - Isso deve finalizar
    */

    // let uniqueMedium = [...new Set(d.medium)];


    // let groupByMedium = data.reduce(
    //     (d,)
    // );
    // let countMedium;


    $: xDomain = data.map((d) => d.medium);
    $: yDomain = data.map((d) => +d.population);
  
    $: yScale = scaleBand().domain(xDomain).range([0, innerHeight]).padding(0.1);
    $: xScale = scaleLinear()
      .domain([0, Math.max.apply(null, yDomain)])
      .range([0, innerWidth]);
  </script>
  
  <svg {width} {height}>
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each xScale.ticks() as tickValue}
        <g transform={`translate(${xScale(tickValue)},0)`}>
          <line y2={innerHeight} stroke="black" />
          <text text-anchor="middle" dy=".7em" y={innerHeight + 3}>
            {tickValue}
          </text>
        </g>
      {/each}
      {#each data as d}
        <text
          text-anchor="end"
          x="-3"
          dy=".3em"
          y={yScale(d.country) + yScale.bandwidth() / 2}
        >
          {d.country}
        </text>
        <rect
          x="0"
          y={yScale(d.country)}
          width={xScale(d.population)}
          height={yScale.bandwidth()}
        />
      {/each}
    </g>
  </svg>
  