<script>
    import { onMount } from 'svelte';
    let refs = [];
    const timeline = [
        { person: 'Amelia', event: 'Born in Hunterdon Medical Center', age: 0 },
        { person: 'Jesse', event: 'Born in Newark University Hospital', age: 0 },
        { person: 'Amelia', event: 'Started pre-school at private Montessori School with ample early learning resources and 1-1 care', age: 4 }, 
        { person: 'Jesse', event: 'Started kindergarten at underfunded program in Newark public schools', age: 5 }, 
        { person: 'Amelia', event: 'Moved to a single-family home in neighborhood with safe drinking water, healthy food options, and well-funded schools', age: 9 },
        { person: 'Jesse', event: 'Moved from apartment to apartment as family was unable to afford rising rent, often near previous or current waste facilities ', age: 10 }, 
        { person: 'Amelia', event: 'Massive hurricane induced by global climate change and rising sea levels hits, and town emergency responders rescue people unable to evacuate on time', age: 13 }, 
        { person: 'Jesse', event: 'Massive hurricane induced by global climate change and rising sea levels hits, and chemical spill from unregulated factory washes harmful toxins into community water and air', age: 13 }, 
        { person: 'Amelia', event: 'Weeks of preparation before standardized state testing week in school', age: 15 }, 
        { person: 'Jesse', event: 'Results of standardized testing are released and show significantly under average performance', age: 15 }, 
        { person: 'Amelia', event: 'College admissions process begins', age: 17 }, 
        { person: 'Jesse', event: 'Considers and hopes to attend college, but cannot afford tuition in single-parent household with many dependents', age: 17 },
        { person: 'Amelia', event: 'Graduates from college with two degrees and well-paying job', age: 24 }, 
        { person: 'Jesse', event: 'Continues to work service sector jobs to pay fluctuating yet rising rent and energy bills due to global warming', age: 25 }, 
        { person: 'Amelia', event: 'Moves to affluent neighborhood with family', age: 30 }, 
        { person: 'Jesse', event: 'Cannot vaccinate during outbreak of contagious influenza strain with no health insurance and no means of transportation to vaccination sites', age: 37 }, 
        { person: 'Amelia', event: 'Vaccinates family with employer-sponsored, high coverage health insurance following outbreak', age: 37 }, 
    ]; 

    onMount(() => {
        const observer = new IntersectionObserver(
            entries => {
                entries.forEach(entry => {
                    if(entry.isIntersecting){
                        entry.target.classList.add('visible');
                        // observer.unobserve(entry.target); 
                    } else {
                      entry.target.classList.remove('visible');
                    }
                }); 
            }, 
            { threshold: 0.3 }
        ); 

        refs.forEach(el => observer.observe(el)); 
   
        return() => {
          observer.disconnect(); 
  
        }
    }); 
</script>

<div class="title">
  <h1>Implications for the Future</h1>
    <p style="max-width: 640px; margin: 1rem auto; padding: 0 1.5rem; font-family: 'EB Garamond', serif; font-size: 1.15rem; line-height: 1.4; text-align: justify;">
      This data is not just numbers on a screen. It represents lived experiences 
      and real-world implications. The two divided paths on this timeline follow the lives of Amelia, a Hunterdon County resident, 
      and Jesse, an Essex County resident. 
      Their experiences reflect what the future could look like if inequality based in 
      social vulnerability continues to be brushed aside, neglected, and forgotten.  
    </p>
</div>

<!-- I used ChatGPT to help understand how to implement each timeline item and make them visible with every scroll. -->
<div class="timeline-container">
  <div class="timeline-line"></div>
  {#each timeline as item, i}
    <div
      class="timeline-item {item.person.toLowerCase()}"
      style="--i: {i}"
      bind:this={refs[i]}
    >
      <div class="card">
        <div class="person">{item.person} (Age {item.age})</div>
        <div class="description">{item.event}</div>
      </div>
    </div>
  {/each}
</div>


<style>
  h1 {
    font-family: 'Libre Baskerville', serif; 
    font-style: italic; 
    margin-top: 5rem; 
  }

  .title {
    display: flex; 
    flex-direction: column;
    justify-content: center; 
    align-items: center;
    text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
  }

    .timeline-container {
        position: relative;
        width: 90%;
        max-width: 1000px;
        margin: 4rem auto;
        padding: 2rem 0;
    }

    .timeline-line {
        position: absolute;
        left: 50%;
        top: 0;
        bottom: 0;
        width: 10px;
        background: black;
        transform: translateX(-50%);
        z-index: 0;
    }

    /* I used ChatGPT with this particular CSS styling to ensure that the transitions were occurring. */
    .timeline-item {
        position: relative;
        width: 50%;
        padding: 1rem 2rem;
        box-sizing: border-box;
        opacity: 0;
        transform: translateY(50px);
        transition: opacity 0.6s ease, transform 0.6s ease;
        will-change: opacity, transform; 
    }

    .timeline-item.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .timeline-item:not(.visible) {
      transform: translateY(-50px);
    }

    .timeline-item.amelia {
        left: 0;
        text-align: right;
    }   

    .timeline-item.jesse {
      left: 50%;
      text-align: left;
    }

    .card {
      background: white;
      border-radius: 0.5rem;
      padding: 1rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      display: inline-block;
      max-width: 90%;
    }

    .amelia .card {
      border-left: 10px solid gray;
    }

    .jesse .card {
      border-right: 10px solid black;
    }

    .person {
      font-weight: bold;
      margin-bottom: 0.5rem;
      color: black;
      font-family: 'Libre Baskerville', serif; 
      font-style: italic; 
      text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
    }

    .description {
      font-size: 1rem;
      color: black;
      font-family: 'EB Garamond', serif; 
      text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
    }
</style>