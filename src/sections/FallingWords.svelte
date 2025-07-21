<script>
    import { fly } from 'svelte/transition'; 
    import { onMount } from 'svelte'; 

    const words = ['social', 'vulnerability', 'cannot', 'be', 'separated', 'from', 'race']; 
    let wordRefs = []; 
    let visibleWords = Array(words.length).fill(false); 
    let rotations = []; 

    onMount(() => {
        rotations = words.map(() => (Math.random() * 30 - 10));
        wordRefs.forEach((el, i) => {
            const observer = new IntersectionObserver(([entry]) => {
                if(entry.isIntersecting){
                    visibleWords[i] = true; 
                    observer.unobserve(entry.target); 
                }
            }, { threshold: 0.5 }); 
            observer.observe(el);
        }); 
    }); 
</script>

<section class="falling-words-container">
  {#each words as word, i}
    <div class="spacer" />
    <div
      class="word-container"
      bind:this={wordRefs[i]}>

      <!-- I used ChatGPT to help understand how to rotate the words as they fall. -->
      {#if visibleWords[i]}
        <span
          in:fly={{ y: -50, duration: 500 }}
          out:fly={{ y: -50, duration: 400 }}
          style="display: inline-block; transform: rotate({rotations[i]}deg);"
        >
          {word}
        </span>
      {/if}
    </div>
  {/each}
</section>

<style>
.falling-words-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem;
}

.word-container {
    min-height: 5rem;
    font-size: 2.8rem;
    font-weight: bold;
    text-align: center;
    font-family: 'Libre Baskerville', serif; 
    font-style: italic; 
    text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.5);
}

.spacer {
  height: 20vh;
}

</style>