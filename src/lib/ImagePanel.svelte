<script>
    export let currentStep = 0; 
    export let images = [];
</script>

<div class="sticky-container">
    {#each images as img, i}
    <img src={img} class="image {currentStep === i ? 'visible' : 'hidden'}"
    alt=""/>
    {/each}
</div>

<style>
    .sticky-container {
        position: sticky; 
        top: 0; 
        height: 100vh; 
        display: flex; 
        flex-direction: column;
        align-items: center; 
        justify-content: center; 
    }

    .image {
        max-width: 80vh; 
        max-height: 80vh; 
        transition: opacity 0.8s ease; 
        position: absolute; 
        border: rgba(0, 0, 0, 0);
        box-shadow: 10px 10px black;
    }

    .image.hidden {
        opacity: 0; 
        pointer-events: none; 
    }

    .image.visible {
        opacity: 1; 
    }
</style>