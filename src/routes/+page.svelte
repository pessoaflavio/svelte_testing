<script>
    // console.log('hi')
    import { onMount } from "svelte";
    import { reduceCategories } from '/src/routes/logicFunction.svelte';
    
    let artists = [];

    onMount(async function () {
        const response = await fetch('src/data/2023_amoeba2.json');
        const data = await response.json();
        console.log(data.artists);
        artists = data.artists;
    });

    $: groupTypes = reduceCategories
    
    
</script>
<style>
main {
    margin: 0;
    box-sizing: content-box;
    font-family: 'IBM Plex Mono';
    display: flex;
    font-size: 10px;
    flex-wrap: wrap;
}
.guest-container{
    background-color: beige;
    padding: 10px;
    margin-bottom: 15px;
    margin-right: 15px;
    width: 300px;
}
h1{
    margin-top: 10px;
    margin-bottom: 10px;
    font-size: 60px;
    font-family: 'IBM Plex Serif';
    font-weight: lighter;
    font-style: italic;
    text-transform: capitalize;
    color: tomato;
}
h2{
    font-size: 12px;
}
.pick {
    color: tomato;
    /* width: 200px; */
}
</style>
<h1>What's in Amoeba's bag?</h1>
<main>
    
  
    {#each artists as artist}
      <div class="guest-container">
        <h2>{artist.guest}</h2>
        <hr>
        <p>
            Picks: {artist.picks.length}
            <!-- calc: {JSON.stringify(groupTypes(artist.picks).val)} -->
        </p>
        {#each Object.entries(groupTypes(artist.picks).val) as calculation}
        <!-- {#each JSON.stringify(groupTypes(artist.picks).val) as calculation} -->
            <svg xmlns="http://www.w3.org/2000/svg" height="25">
                <rect width="{calculation[1]*20}" height="7" fill="coral" />
                <text x="0" y="17" fill="black">{calculation[0]} / {calculation[1]}</text>
            </svg>
            <!-- <div style="width:{calculation[1]*10}; height:10px; margin-bottom: 2px; background-color:white">
            {calculation}
            </div> -->
        {/each} 
        <div>

        </div>
        <!-- <hr>
            {#each artist.picks as pick}
                <p class="pick">
                    
                    W: {JSON.stringify(pick.album)} 
                    A: {JSON.stringify(pick.artist)}
                    M: {JSON.stringify(pick.medium)} 

                    <!-- testing: {groupTypes(pi)} -->
                <!-- </p>
                <hr style="height:1px;border:none;background-color:#ffcc99">    
            {/each}  -->
      </div>
    {/each}
  </main>