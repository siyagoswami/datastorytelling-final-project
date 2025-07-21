<script lang="ts">
    import { onMount } from 'svelte';
    export let imageUrl: string = ''; 
    export let altText: string = ''; 
    export let transitionDuration: string = '3s';
    export let height: string = '100vh'; 

    let imageElement: HTMLDivElement; 
    let isVisible = false; 

    onMount(() => {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach((entry) => {
                if(entry.isIntersecting){
                    isVisible = true; 
                    observer.unobserve(entry.target);
                }
            });
        }, { threshold: 0.6 }); 

        if(imageElement) observer.observe(imageElement); 
        return () => observer.disconnect();
    });
</script>

<div class="image-container" bind:this={imageElement}>
    <img src={imageUrl} alt={altText} 
    style="--blur: {isVisible ? '0px' : '8px'}">
</div>


<style>
    .image-container {
        height: 100vh; 
        position: relative; 
        overflow: hidden; 
    }

    img {
        width: 100%; 
        height: 100%; 
        object-fit: cover; 
        filter: blur(var(--blur)); 
        transition: filter 4s ease; 
    }
</style>