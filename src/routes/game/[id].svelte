<script>
// @ts-nocheck


    import { page } from "$app/stores";
    import maps from "$lib/maps.json";
    import pchallenge from "$lib/pchallenge.json";
    import tchallenge from "$lib/tchallenge.json";
    import demonImg from "$lib/demon.png";

    const maps_data = maps;

    const pchallenge_data = Object.keys(pchallenge);
    const tchallenge_data = Object.keys(tchallenge);

    const pchallege_tool = Object.values(pchallenge);
    const tchallenge_tool = Object.values(tchallenge);

    const two_team = "TEAMCHALLENGERS";
    const two_player = "CHALLENGER";
    const reroll_block = "KEINE KERZEN";

    const alptraum = "SCHLAFPARALYSE"


    let players = parseInt($page.params.id);

    let player_name1 = "Player 1";
    let player_name2 = "Player 2";
    let player_name3 = "Player 3";
    let player_name4 = "Player 4";
    
    let team_challenge;
    let team_challenge_1;
    let team_challenge_2;
    let player_challenge1;
    let player_challenge1_1;
    let player_challenge1_2;
    let player_challenge2;
    let player_challenge2_1;
    let player_challenge2_2;
    let player_challenge3;
    let player_challenge3_1;
    let player_challenge3_2;
    let player_challenge4;
    let player_challenge4_1;
    let player_challenge4_2;
    let team_tooltip;
    let team_tooltip_1;
    let team_tooltip_2;
    let p1_tooltip;
    let p1_tooltip_1;
    let p1_tooltip_2;
    let p2_tooltip;
    let p2_tooltip_1;
    let p2_tooltip_2;
    let p3_tooltip;
    let p3_tooltip_1;
    let p3_tooltip_2;
    let p4_tooltip;
    let p4_tooltip_1;
    let p4_tooltip_2;

    let team_rand;
    let player1_rand;
    let player2_rand;    
    let player3_rand;
    let player4_rand;

    let random_map;
    const difficulties = ["Amateur", "Fortgeschritten", "Professionell"];
    let difficulty;

    let health = 10;
    let max_health = 10;
    let rerolls = 10;
    let max_rerolls = 10;
    let coins = 0;

    newRound();
    
    function newRound() {
        
        team_rand = parseInt(Math.floor(Math.random() * tchallenge_data.length));
        team_challenge = tchallenge_data[parseInt(team_rand)];
        team_tooltip = tchallenge_tool[team_rand];
        
        do {
        team_rand = parseInt(Math.floor(Math.random() * tchallenge_data.length));
        team_challenge_1 = tchallenge_data[parseInt(team_rand)];
        team_tooltip_1 = tchallenge_tool[team_rand];
        
        
        team_rand = parseInt(Math.floor(Math.random() * tchallenge_data.length));
        team_challenge_2 = tchallenge_data[parseInt(team_rand)];
        team_tooltip_2 = tchallenge_tool[team_rand];
        } while (team_challenge_1 === team_challenge || team_challenge_2 === team_challenge_1 || team_challenge_2 === team_challenge);
        
        player1_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge1 = pchallenge_data[player1_rand];
        p1_tooltip = pchallege_tool[player1_rand];

        do {
        player1_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge1_1 = pchallenge_data[player1_rand];
        p1_tooltip_1 = pchallege_tool[player1_rand];
        
        player1_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge1_2 = pchallenge_data[player1_rand];
        p1_tooltip_2 = pchallege_tool[player1_rand];
        } while (player_challenge1 === player_challenge1_1 || player_challenge1 === player_challenge1_2 || player_challenge1_1 === player_challenge1_2);
        
        player2_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge2 =  pchallenge_data[player2_rand];
        p2_tooltip = pchallege_tool[player2_rand];
        
        do {
        player2_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge2_1 =  pchallenge_data[player2_rand];
        p2_tooltip_1 = pchallege_tool[player2_rand];
        
        player2_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge2_2 =  pchallenge_data[player2_rand];
        p2_tooltip_2 = pchallege_tool[player2_rand];
        } while (player_challenge2 === player_challenge2_1 || player_challenge2 === player_challenge2_2 || player_challenge2_1 === player_challenge2_2);

        player3_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge3 =  pchallenge_data[player3_rand];
        p3_tooltip = pchallege_tool[player3_rand];
        
        do {
        player3_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge3_1 =  pchallenge_data[player3_rand];
        p3_tooltip_1 = pchallege_tool[player3_rand];

        player3_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge3_2 =  pchallenge_data[player3_rand];
        p3_tooltip_2 = pchallege_tool[player3_rand];
        } while (player_challenge3 === player_challenge3_1 || player_challenge3 === player_challenge3_2 || player_challenge3_1 === player_challenge3_2);

        player4_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge4 =  pchallenge_data[player4_rand];
        p4_tooltip = pchallege_tool[player4_rand];
        
        do {
        player4_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge4_1 =  pchallenge_data[player4_rand];
        p4_tooltip_1 = pchallege_tool[player4_rand];
        
        player4_rand = parseInt(Math.floor(Math.random() * pchallenge_data.length));
        player_challenge4_2 =  pchallenge_data[player4_rand];
        p4_tooltip_2 = pchallege_tool[player4_rand];
        } while (player_challenge3 === player_challenge3_1 || player_challenge3 === player_challenge3_2 || player_challenge3_1 === player_challenge3_2);

        random_map = maps_data[parseInt(Math.floor(Math.random() * maps_data.length))];

        difficulty = difficulties[parseInt(Math.floor(Math.random() * difficulties.length))];

        if (team_challenge === alptraum || (team_challenge === two_team && team_challenge_1 === alptraum) || (team_challenge === two_team && team_challenge_2 === alptraum))
        {
            difficulty = "ALBTRAUM";
        }
    }
    
    function doReroll() {
        if (rerolls > 0) {
            rerolls--;
            newRound();
        } else if (rerolls == 0) {
            if (health > 1) {
                health--;
                newRound();
            }
        }
    }
    
    function addHealth() {
        health = health + 1;
        if (health > max_health) {
            health = max_health;
        }
    }

    function removeHealth() {
        health = health - 1;
        if (health < 0) {
            health = 0;
        }
    }

    function addReroll() {
        rerolls = rerolls + 1;
        if (rerolls > max_rerolls) {
            rerolls = max_rerolls;
        }
    }

    function removeReroll() {
        rerolls = rerolls - 1;
        if (rerolls < 0) {
            rerolls = 0;
        }
    }

    function addCoin() {
        coins = coins + 1;
    }

    function removeCoin() {
        if (coins > 0) {
            coins = coins - 1;
        }
    }

    function addMaxHealth() {
        max_health = max_health + 1;
    }

    function removeMaxHealth() {
        max_health = max_health - 1;
        if (max_health < 0) {
            max_health = 0;
        }
        if (health > max_health) {
            health = max_health;
        }
    }

    function addMaxReroll() {
        max_rerolls = max_rerolls + 1;
        
    }

    function removeMaxReroll() {
        max_rerolls = max_rerolls - 1;
        if (max_rerolls < 0) {
            max_rerolls = 0;
        }
        if (rerolls > max_rerolls) {
            rerolls = max_rerolls;
        }
    }

    function buyReroll() {
        if (coins >= 6) {
            coins = coins - 6;
            addReroll();
        }
    }

    function buyMaxReroll() {
        if (coins >= 6) {
            coins = coins - 12;
            addMaxReroll();
        }
    }

    function buyHealth() {
        if (coins >= 10) {
            coins = coins - 10;
            addHealth();
        }
    }

    function buyMaxHealth() {
        if (coins >= 20) {
            coins = coins - 20;
            addMaxHealth();
        }
    }
    
    
    </script>
    
    <div class="index">
        <h1>Phasmo Challenges</h1>
        <div class="stats">
            <div class="health">
            <progress id="health" value={health} max={max_health}></progress>
            <p>{health}/{max_health}</p>
        </div>
        <div class="coins">
            <p>Coins:</p>
            <p>{coins}</p>
        </div>
        <div class="rerolls">
            <progress id="rerolls" value={rerolls} max={max_rerolls}></progress>
            <p>{rerolls}/{max_rerolls}</p>
        </div>
        </div>


        <h3>Team Challenge</h3>
        <p title={team_tooltip}>{team_challenge}</p>
        {#if team_challenge === two_team}
            <p title={team_tooltip_1}>{team_challenge_1}</p>
            <p title={team_tooltip_2}>{team_challenge_2}</p>
        {/if}
        <div class="map">
            <p>Map: {random_map}</p>
            {#if difficulty === "ALBTRAUM"}
                <p style="color:blueviolet; font-weight:bold">Difficulty: {difficulty} <img style="color:blueviolet;" src={demonImg} alt="Demon" width=15px height=15px></p>
            {:else}
                <p>Difficulty: {difficulty}</p>
            {/if}
            
        </div>
        <br>
        <div class="players">
            {#if players > 0}
            <div class="player">
                <h5><input type="text" name="player1" id="player1" bind:value={player_name1}></h5>
                <p title={p1_tooltip}>{player_challenge1}</p>
                {#if player_challenge1 === two_player}
                <p title={p1_tooltip_1}>{player_challenge1_1}</p>
                <p title={p1_tooltip_2}>{player_challenge1_2}</p>
                {/if}

            </div>
            {/if}
            {#if players > 1}
            <div class="player">
                <h5><input type="text" name="player1" id="player1" bind:value={player_name2}></h5>
                <p title={p2_tooltip}>{player_challenge2}</p>
                {#if player_challenge2 === two_player}
                <p title={p2_tooltip_1}>{player_challenge2_1}</p>
                <p title={p2_tooltip_2}>{player_challenge2_2}</p>
                {/if}
            </div>
            {/if}
            {#if players > 2}
            <div class="player">
                <h5><input type="text" name="player1" id="player1" bind:value={player_name3}></h5>
                <p title={p3_tooltip}>{player_challenge3}</p>
                {#if player_challenge3 === two_player}
                <p title={p3_tooltip_1}>{player_challenge3_1}</p>
                <p title={p3_tooltip_2}>{player_challenge3_2}</p>
                {/if}
            </div>
            {/if}
            {#if players > 3}
            <div class="player">
                <h5><input type="text" name="player1" id="player1" bind:value={player_name4}></h5>
                <p title={p4_tooltip}>{player_challenge4}</p>
                {#if player_challenge4 === two_player}
                <p title={p4_tooltip_1}>{player_challenge4_1}</p>
                <p title={p4_tooltip_2}>{player_challenge4_2}</p>
                {/if}
            </div>
            {/if}
        </div>
        <div class="buttons">
            <button class="RowI" on:click={newRound}>New Round</button>
            {#if health > 1 || rerolls > 0}
            <button class="RowI" on:click={doReroll}>Reroll</button>
            {:else}
            <button class="RowI" disabled on:click={doReroll}>Reroll</button>
            {/if}
        </div>
        <div class="buttons">
            <button class="RowII" on:click={addHealth}>Health +</button>
            <button class="RowII" on:click={removeHealth}>Health -</button>
            <button class="RowII" on:click={addReroll}>Reroll +</button>
            <button class="RowII" on:click={removeReroll}>Reroll -</button>
        </div>
        <div class="buttons">
            <button class="RowIII" on:click={addCoin}>Coin +</button>
            <button class="RowIII" on:click={removeCoin}>Coin -</button>
        </div>
        <div class="buttons">
            <button class="RowIII" on:click={addMaxHealth}>Max Health +</button>
            <button class="RowIII" on:click={removeMaxHealth}>Max Health -</button>
            <button class="RowIII" on:click={addMaxReroll}>Max Reroll +</button>
            <button class="RowIII" on:click={removeMaxReroll}>Max Reroll -</button>
        </div>
        <div class="buttons">
            {#if coins >= 6}
            <button class="RowIV" on:click={buyReroll}>Buy Reroll (6)</button>
            {:else}
            <button class="RowIV" disabled on:click={buyReroll}>Buy Reroll (6)</button>
            {/if}
            {#if coins >= 12}
            <button class="RowIV" on:click={buyMaxReroll}>Buy Max Reroll (12)</button>
            {:else}
            <button class="RowIV" disabled on:click={buyMaxReroll}>Buy Max Reroll (12)</button>
            {/if}
            {#if coins >= 10}
            <button class="RowIV" on:click={buyHealth}>Buy Health (10)</button>
            {:else}
            <button class="RowIV" disabled on:click={buyHealth}>Buy Health (10)</button>
            {/if}
            {#if coins >= 20}
            <button class="RowIV" on:click={buyMaxHealth}>Buy Max Health (20)</button>
            {:else}
            <button class="RowIV" disabled on:click={buyMaxHealth}>Buy Max Health (20)</button>
            {/if}
        </div>
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
    .players {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        width: 100%;
    }
    .player {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 25%;
        border: 1px dotted;
    }
    .player h5 {
        font-size: 1.5rem;
        margin: 0;
    }
    
    .player h5 input {
        font-size: 1.0rem;
        margin: 0;
        border: none;
        background: none;
        outline: none;
        width: 100%;
        text-align: center;
        font-family: 'Fredoka', sans-serif;
        font-weight: bold;
    }
    .buttons {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        width: 100%;
    }
    .buttons button{
        width: 25%;
        border: 1px solid;
        border-radius: 5px;
        background: none;
        outline: none;
        margin: 5px;
        font-size: 1.5rem;
        font-family: 'Fredoka', sans-serif;
        font-weight: bold;
    }
    .buttons button:hover {
        background: #f5f5f5;
        cursor: pointer;
    }

    .health progress {
        width: 100%;
        height: 10px;
        background: #f5f5f5;
        border: 1px solid;
        border-radius: 5px;
        margin: 5px;
    }

    .health {
        width: 100%;
        height: 10px;
        border: none;
        margin: 5px;
        text-align: center;
    }

    .rerolls {
        width: 100%;
        height: 10px;
        border: none;
        margin: 5px;
        text-align: center;
    }

    .coins {
        width: 100%;
        height: 70px;
        border: none;
        margin: 5px;
        text-align: center;
    }

    .rerolls progress {
        width: 100%;
        height: 10px;
        background: #f5f5f5;
        border: 1px solid;
        border-radius: 5px;
        margin: 5px;
    }

    .stats {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        width: 100%;
    }
    .stats div {
        width: 25%;
    }

    .map {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        border: 1px solid;
        padding: 0px 10px;
    }

    img {
        filter: invert(23%) sepia(53%) saturate(4584%) hue-rotate(263deg) brightness(88%) contrast(101%);
    }
    .health progress::-moz-progress-bar { background: red; }
    .health progress::-webkit-progress-value { background: red; }
    .rerolls progress::-moz-progress-bar { background: blue; }
    .rerolls progress::-webkit-progress-value { background: blue; }

    </style>