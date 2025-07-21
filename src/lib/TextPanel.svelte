<script>
    import { createEventDispatcher, onMount } from 'svelte';
    let container; 
    const dispatch = createEventDispatcher();

    onMount(() => {
        const observer = new IntersectionObserver(([entry]) => 
            {
                if(entry.isIntersecting) dispatch('enter');
            }, 
            { threshold: 0.5, }
        ); 
        
        if(container)observer.observe(container);
        return () => observer.disconnect(); 
    }); 
</script>

<section bind:this={container}>
    <slot/>
</section>

<style>
    section {
        min-height: 80vh; 
        display: flex; 
        align-items: center; 
        padding: 1.45rem; 
        font-size: 1.1rem; 
        font-family: 'EB Garamond', serif;
        box-shadow: 8px 10px black;
    }
</style>