<script>
    // console.log('hi')
    import { onMount } from "svelte";

    let artists = [];

    onMount(async function () {
        const response = await fetch('src/data/2023_amoeba2.json');
        const data = await response.json();
        console.log(data.artists);
        artists = data.artists;
    });
    


    // function handleMouseOver(event) {
    //     o

    // }
    
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
    font-size: 20px;
}
h2{
    font-size: 12px;
}
.pick {
    color: tomato;
    /* width: 200px; */
}
</style>
<h1>AMOEBA WHAT'S IN MY BAG</h1>
<main>
    
  
    {#each artists as artist}
      <div class="guest-container">
        <h2>{artist.guest}</h2>
        <hr>
        <p>
            Picks: {artist.picks.length}
        </p>
        <hr>
            {#each artist.picks as pick}
                <p class="pick">
                    
                    W: {JSON.stringify(pick.album)} 
                    A: {JSON.stringify(pick.artist)}
                    M: {JSON.stringify(pick.medium)} 
                </p>
                <hr style="height:1px;border:none;background-color:#ffcc99">    
            {/each} 
      </div>
    {/each}
  </main>