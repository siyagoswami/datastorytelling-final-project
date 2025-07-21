<script>
    export let phase = 'idle'; 
</script>

<div class="scene">
    <img src="amelia.png"
    alt="Hunterdon character"
    class="character hunterdon"
    class:walk-out={phase === 'out'}
    class:walk-back={phase === 'back'}/>

    <img src="jesse.png"
    alt="Essex character"
    class="character essex"
    class:walk-out={phase === 'out'}
    class:walk-back={phase === 'back'}/>

    {#if phase === 'back'}
        <p class="final-line">But... it doesn't have to be this way.</p>
    {/if}
</div>

<style>
    .scene {
        position: relative; 
        width: 100%; 
        height: 300px; 
        /* background: #f4f4f4;  */
        overflow: hidden; 
    }

    .character {
        position: absolute; 
        bottom: 0; 
        width: 200px; 
        will-change: transform; 
    }

    .essex {
        left: 50%;
        transform: translateX(60%) scaleX(1); 
    }

    .hunterdon {
        left: 50%;
        transform: translateX(-120%) scaleX(-1); 
    }

    .walk-out.essex {
        animation: out-right 10s forwards;
    }

    .walk-out.hunterdon {
        animation: out-left 10s forwards;
    }

    .walk-back.essex {
        animation: back-right 8s forwards;
    }

    .walk-back.hunterdon {
        animation: back-left 8s forwards;
    }

    .final-line {
        text-align: center;
        margin-top: 0.5rem;
        font-size: 1.8rem;
        font-weight: 500;
        opacity: 0;
        animation: fadeIn 8s ease forwards;
        font-family: 'Libre Baskerville', serif; 
        font-style: italic; 
        text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
    }

    /* I used ChatGPT to help me understand how to integrate KeyFrames and move the characters back and forth. */
    /* Animations */
    @keyframes out-left {
        to { transform: translateX(-280%) scaleX(-1); }
    }

    @keyframes out-right {
        to { transform: translateX(180%) scaleX(1); }
    }

    @keyframes back-left {
        from { transform: translateX(-280%) scaleX(1); }
        to { transform: translateX(-120%) scaleX(1); }
    }

    @keyframes back-right {
        from { transform: translateX(180%) scaleX(-1); }
        to { transform: translateX(60%) scaleX(-1); }
    }

    @keyframes fadeIn {
    to {
        opacity: 1;
    }
}
</style>