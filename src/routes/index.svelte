<script>

export let players = 1;



</script>

<div class="index">
    <h1>Phasmo Challenges</h1>
    <h3>Choose Players:</h3>
    <input bind:value={players} type="number" name="Players" id="players" min=1 max=4>

    <a href="game/{players}">Start Game</a>
</div>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@300&display=swap');
.index {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    font-family: 'Fredoka', sans-serif;
}
a {
    background-color: #f5f5f5;
    border: none;
    border-radius: 5px;
    padding: 10px;
    font-size: 1.2em;
    font-weight: bold;
    text-decoration: none;
    color: #000;
    margin: 10px;
}
</style>