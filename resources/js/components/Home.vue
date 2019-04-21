<template>
<div class="container h-100">
    <div class="row panel scores">
        <div class="score pikachu pt-3 ">
            <img src="../../../public/img/pikachudefault.gif" id="pikachuDefault" alt="pikachuDefault">
            <h1 class="mr-5">Pikachu</h1>
            <div class="life-bar">
                <div class="life" :class="{danger: pokemonLife1 < 20}" :style="{width: pokemonLife1 + '%'}">
                </div>
            </div>
            <div class="mr-5">{{pokemonLife1}}%</div>
        </div>
        <div class="score">
            <img src="../../../public/img/latios.gif" alt="Latios">
            <h1>Latios</h1>
            <div class="life-bar">
                <div class="life" :class="{danger: pokemonLife2 < 20}" :style="{width: pokemonLife2 + '%'}">
                </div>
            </div>
            <div>{{pokemonLife2}}%</div>
        </div>
    </div>
    <div class="container">
        <div v-if="hasResult" class="panel result">
            <div v-if="pokemonLife2 == 0" class="win">You won the battle!</div>
            <div v-else class="lose">You lost the battle!</div>
        </div>
    </div>
    <div class="row panel buttons">
        <div v-if="running">
            <button @click="attack1(true)" onclick="pikachuQuickAttack()" class="btn quick-attack col mb-2">Quick Attack</button>
            <button @click="attack(true)" onlick="pikachuVoltTackle()" class="btn volt-tackle col mb-2">Volt Tackle</button>
            <button @click="attack3(true)" class="btn iron-tail col mb-2">Iron Tail</button>
            <button @click="attack2(true)" class="btn thunder-bolt col mb-2">Thunderbolt</button>
            <button @click="healAndHurt" class="btn heal col mb-2">Hp Potion</button>
            <button @click="running = false" class="btn give-up col mb-2">Quit Battle</button>
        </div>
        <button v-else @click="startBattle" class="btn new-battle">Start Battle</button>
    </div>
    <div class="row">
        <div v-if="logs.length" class="container panel logs">
            <ul>
                <li v-for="(log,key) in logs" :key = "key" :class="log.cls" class="log ">{{ log.text }}</li>
            </ul>
        </div>
    </div>
    
</div>
</template>   

<script>

export default {

    data(){
        return {
        
        running: false,   
        pokemonLife1: 100,
        pokemonLife2: 100,
        logs: []
       
        }
    },
    computed: {
         hasResult() {
            return this.pokemonLife1 == 0 || this.pokemonLife2 == 0
        },
    },
    methods: {
        
        startBattle() {
            this.running = true
            this.pokemonLife1 = 100
            this.pokemonLife2 = 100
            this.logs = []


        },
        /* 	begin volt tackle */
        attack(voltTackle) {
            this.hurt('pokemonLife2', 2, 5, voltTackle, 'Volt Tackle', 'Pikachu', 'Latios', 'pokemon1')
            if (this.pokemonLife2 > 0) {
                this.hurt('pokemonLife1', 8, 15, false, 'Giga Impact', 'Latios', 'Pikachu', 'pokemon2')
            }
        },

        hurt(atr, min, max, voltTackle, attack, source, target, cls) {
            const plus = voltTackle ? 5 : 0
            const hurt = this.getRandom(min + plus, max + plus)
            this[atr] = Math.max(this[atr] - hurt, 0)
            this.registerLog(`${source} used ${attack}! 
            ${target} lost ${hurt} HP!`, cls)
        },

        /* finish volt tackle */

        /* 	begin Quick Attack */
        attack1(quickAttack) {
            this.hurt('pokemonLife2', 1, 2, quickAttack, 'Quick Attack', 'Pikachu', 'Latios', 'pokemon1')
            if (this.pokemonLife2 > 0) {
                this.hurt('pokemonLife1', 7, 12, false, 'Luster Purge', 'Latios', 'Pikachu', 'pokemon2')
            }
        },

        hurt1(atr, min, max, quickAttack, attack, source, target, cls) {
            const plus = quickAttack ? 5 : 0
            const hurt = this.getRandom(min + plus, max + plus)
            this[atr] = Math.max(this[atr] - hurt, 0)
            this.registerLog(`${source} used ${attack}! 
            ${target} lost ${hurt} HP!`, cls)
        },

        /* finish Quick Attack */

        /* 	begin ironTail */

        attack3(ironTail) {
            this.hurt('pokemonLife2', 4, 8, ironTail, 'Iron Tail', 'Pikachu', 'Latios', 'pokemon1')
            if (this.pokemonLife2 > 0) {
                this.hurt('pokemonLife1', 7, 12, false, 'Giga Impact', 'Latios', 'Pikachu', 'pokemon2')
            }
        },

        hurt3(atr, min, max, ironTail, attack, source, target, cls) {
            const plus = ironTail ? 5 : 0
            const hurt = this.getRandom(min + plus, max + plus)
            this[atr] = Math.max(this[atr] - hurt, 0)
            this.registerLog(`${source} used ${attack}! 
            ${target} lost ${hurt} HP!`, cls)
        },

        /* Finish ironTail */

        /* 	Begin thunderBolt */

        attack2(thunderBolt) {
            this.hurt('pokemonLife2', 4, 8, thunderBolt, 'Thunder Bolt', 'Pikachu', 'Latios', 'pokemon1')
            if (this.pokemonLife2 > 0) {
                this.hurt('pokemonLife1', 7, 12, false, 'Luster Purge', 'Latios', 'Pikachu', 'pokemon2')
            }
        },

        hurt2(atr, min, max, thunderBolt, attack, source, target, cls) {
            const plus = thunderBolt ? 5 : 0
            const hurt = this.getRandom(min + plus, max + plus)
            this[atr] = Math.max(this[atr] - hurt, 0)
            this.registerLog(`${source} used ${attack}! 
            ${target} lost ${hurt} HP!`, cls)
        },

        /* Finish thunderBolt */

        /* Begin Heals */
        healAndHurt() {
            this.heal(10, 15)
            this.hurt('pokemonLife1', 7, 12, false, 'Giga Impact', 'Latios', 'Pikachu', 'pokemon2')
        },

        heal(min, max) {
            const heal = this.getRandom(min, max)
            this.pokemonLife1 = Math.min(this.pokemonLife1 + heal, 100)
            this.registerLog(`Pikachu restored ${heal} HP using HP Potion.`, 'pokemon1')
        },

        /* Finish Heals */

        /* Begin Random Math */

        getRandom(min, max) {
            const value = Math.random() * (max - min) + min
            return Math.round(value)
        },

        /* Finish Random Math */

        /* Begin Logs */

        registerLog(text, cls) {
            this.logs.unshift({ text, cls })
        },

        /* Finish logs */


    },
    watch: {
        hasResult(value) {
            if (value) this.running = false
        }
    }

}
</script>

<style>

/* Main */

html, body{
    font-family: 'Open Sans', sans-serif;
    background-image: url('../../../public/img/bg-main2.jpg');
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    background-repeat: no-repeat;
}

#app {
    display: flex;
    flex-direction: column;    
}

.panel {
    margin: 20px;
    padding: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.226);
}

/* Score Area */

.scores {
    display: flex;
    padding-top: 10%;
    background-image: url('../../../public/img/bg4.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;

}

.score {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.score h1 {
    font-weight: 300;
    font-size: 1.6rem;
}

.life-bar{
    width: 80%;
    height: 20px;
    border: 1px solid #AAA;
}

.life-bar .life{
    display: flex;
    justify-content: center;
    height: 100%;
    background-color: rgb(39, 216, 69); 
}

.life-bar .life.danger {
    background-color: red;
}

/* Result Area */

.result {
    display: flex;
    justify-content: center;
    font-size: 1.3rem;
    font-weight: 600;
}

.result .win {
    color: green;
    font-weight: 400;
}

.result .lose{
    color:red;
}

/* Buttons Area */

.buttons{
    display: flex;
    justify-content: center;
    
}

.btn {
    padding: 5px 10px;
    margin: 0px 10px;
    border-radius: 5px;
    text-transform: uppercase;
    font-size: 1.1rem;
}

.new-battle {
    border-color: rgb(4, 67, 150);
    background: linear-gradient(#586ad3,#1432d8);
    color: #fff;
}

.quick-attack {
    border-color: #79794E;
    background: linear-gradient(#a8a878,#8a8a59);
    color: #FFF;
    
}

.volt-tackle {
    border-color: #C19B07;
    background: linear-gradient(#f8d030,#f0c108);
    color: #FFF;
}

.iron-tail {
    border-color: #7A7AA7;
    background: linear-gradient(#b8b8d0,#9797ba);
    color:#FFF;
}

.thunder-bolt {
    border-color: #C19B07;
    background: linear-gradient(#f8d030,#f0c108);
    color: #FFF;
}

.heal {
    border-color: #4A892B;
    background: linear-gradient(#78c850,#5ca935);
    color: #FFF;
}

.give-up {
    border-color: rgb(87, 88, 88);
    background: linear-gradient(#9e9e9e,#797878);
    color: #FFF;
}

/* Logs Area */

.logs ul {
    display: flex;
    flex-direction: column;
    list-style: none;
    padding: 0;
    margin: 0;
}

.logs ul li {
    display: flex;
    justify-content: center;
    margin: 4px 0px;
    padding: 3px 0px;
    font-weight: 400;
    font-size: 1.1rem;
    border-radius: 3px;
}

.pokemon1 {
    background-color: #2f42afcb;
    color: #fff;
}

.pokemon2 {
    background-color: #bd2d32d3;
    color: #fff;
}

/* Responsivity */

@media all and (max-width: 479px) {

.panel .scores{
    position: relative;
    width: 100%;
    height: 100%;
    margin: 0px 0px;
}
}



</style>
