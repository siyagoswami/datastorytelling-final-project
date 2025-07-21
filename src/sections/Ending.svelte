<script lang="ts">
    import { fade } from 'svelte/transition';
    import { onMount } from 'svelte';

    // Sources: https://www.hcnj.us/roads-and-public-property/engineering/the-essex-hudson-greenway/, https://essexcountynj.org/division-of-housing-community-development/, https://www.newarknj.gov/card/rooted-in-newark
    let steps = [
        {
            src: 'https://www.hcnj.us/wp-content/uploads/2022/05/Greenway-Map.jpg',
            caption: 'Construction of Essex-Hudson Greenway, a 9-mile urban park connecting 8 Essex communities to improve transportation and environmental quality'
        }, 
        {
            src: 'https://cdn.prod.website-files.com/57ada58371bead8852a659ad/5e39aee7e0f8591d4f96096c_Unknown.png', 
            caption: 'More allocation of funding toward production of affordable housing units, as well as eligibility for loans through the Homebuyer Assistance Program'
        }, 
        {
            src: 'https://onetreeplanted.org/cdn/shop/files/Youth_Engagement.jpg?v=1738151757', 
            caption: 'Rooted in Newark Initiative, aiming to plan at least 5,000 trees to mitigate the build-up of an urban heat island and effects of carbon heat trapping'
        }
    ]; 

    let visibleSteps = Array(steps.length).fill(false); 
    let imageRefs = []; 

    onMount (() => {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                const target = entry.target as HTMLElement;
                if(entry.isIntersecting){
                    entry.target.classList.add('visible');
                } else {
                    entry.target.classList.remove('visible');
                }
            }); 
        }, { threshold: 0.4 }); 
        
        imageRefs.forEach((el) => observer.observe(el)); 
    }); 

</script>

<div class="ending-text-column">
    <p>Just half of the average life of these two hypothetical residents are so incredibly different. 
        It is dificult to erase or even change centuries of history and inequality. 
        We cannot exactly flick a switch or snap our fingers to make Essex County a safer, 
        more secure place to live. We cannot erase the years of systemic inequality that have given 
        Hunterdon County residents more protection and stability during disruptive times. 
    <br/><br/>
        However, the future is already upon us, and the time to act is now. Although 
        9 million people, myself included, may not be able to change the fact that New Jersey is our home, 
        we certainly <strong>can</strong> build a better home for us, and the people that 
        come after us. 
    <br/><br/>
        Luckily, Essex County residents and the New Jersey State Government are already working to rebuild 
        the narratives of so many Black individuals and families by turning social 
        vulnerability into <strong>community power.</strong> This is of the utmost importance as we continue 
        to live with the realities of our ever-changing world.  
    </p>
</div>

<section class="image-row">
    {#each steps as step, i}
    <div class="photo-step {visibleSteps[i] ? 'visible' : ''}" bind:this={imageRefs[i]}
    data-index={i}>

    <img src={step.src} alt={step.caption} transition:fade={{ duration: 600 }}/> 
    <p class="caption" transition:fade>{step.caption}</p>
    </div>
    {/each}
</section>

<div class="ending-line">
    <h1>1 state. 2 different counties. 1 shared, sustainable reality.</h1>
</div>

<style>
.ending-text-column {
    max-width: 640px;
    margin: 2rem auto;
    padding: 0 1.5rem;
    font-family: 'EB Garamond', serif;
    font-size: 1.15rem;
    line-height: 1.4;
    text-align: justify;
}

.image-row {
    display: flex; 
    flex-direction: row;
    flex-wrap: wrap; 
    justify-content: center; 
    gap: 2rem; 
    padding: 2rem; 
}

/* I referenced ChatGPT for the .photo-step styling in order to get the image and caption neatly in order. */
.photo-step {
    max-width: 300px; 
    flex: 1 1 300px; 
    text-align: center; 
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.6s ease;
}

.photo-step.visible {
    opacity: 1;
    transform: translateY(0);
}

.photo-step:not(.visible) {
    transform: translateY(-30px);
}

.photo-step img {
    width: 100%; 
    height: auto; 
    border-radius: 8px; 
}

.caption {
    margin-top: 0.75rem; 
    font-family: 'EB Garamond', serif; 
    font-size: 1rem; 
    color: black; 
}

.ending-line {
    text-align: center;
    margin-top: 0.5rem;
    padding-bottom: 2rem;
    font-size: 1.5rem;
    opacity: 1;
    font-family: 'Libre Baskerville', serif; 
    font-style: italic; 
    text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
}

@media (max-width: 768px) {
  .image-row {
    flex-direction: column;
    align-items: center;
  }
}

</style>