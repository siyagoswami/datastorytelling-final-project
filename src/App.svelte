<script lang="ts">
  import { onMount } from "svelte";
  import MapSection from "./sections/MapSection.svelte";
  import StorySection from "./sections/StorySection.svelte";
  import ImageSection from "./sections/ImageSection.svelte";
  import SVISection from "./sections/SVISection.svelte";
  import FallingWords from "./sections/FallingWords.svelte";
  import DataViz from "./sections/DataViz.svelte";
  import Timeline from "./sections/Timeline.svelte";
  import Animation from "./sections/Animation.svelte";
  import Ending from "./sections/Ending.svelte";
  
  let phase = 'idle'; 
  let walkOutTrigger;
  let walkBackTrigger; 

  type ZoomTarget = {
    center: [number, number];
    zoom: number;
  };

  let zoomTarget: ZoomTarget = {
    center: [-74.4057, 40.0573],
    zoom: 6,
  };

  let sectionState: HTMLElement;
  let sectionCountyA: HTMLElement;
  let sectionCountyB: HTMLElement;
  let sectionDone: HTMLElement;
  let activeOverlay = "state";

  onMount(() => {
    const options = {
      threshold: 0.5,
    };

    const observer = new IntersectionObserver(
      (entries) => {
        for (const entry of entries) {
          if (entry.isIntersecting) {
            if (entry.target === sectionState) {
              zoomTarget = {
                center: [-74.4057, 40.0583],
                zoom: 6,
              };
              activeOverlay = "state";
            } else if (entry.target === sectionCountyA) {
              zoomTarget = {
                center: [-74.9209, 40.567],
                zoom: 10,
              };
              activeOverlay = "countyA";
            } else if (entry.target === sectionCountyB) {
              zoomTarget = {
                center: [-74.2649, 40.7947],
                zoom: 10,
              };
              activeOverlay = "countyB";
            } else if (entry.target === sectionDone) {
              activeOverlay = "done";
            }
          }
        }
      },
      { threshold: 0.5 }
    );

    const outObserver = new IntersectionObserver(([entry]) => {
          if(entry.isIntersecting){
            phase = 'out'; 
          }
        }, { threshold: 0.5 }); 

    const backObserver = new IntersectionObserver(([entry]) => {
          if(entry.isIntersecting){
            phase = 'back'; 
          }
        }, { threshold: 0.5 }); 

        if(walkOutTrigger) outObserver.observe(walkOutTrigger); 
        if(walkBackTrigger) backObserver.observe(walkBackTrigger); 

    observer.observe(sectionState);
    observer.observe(sectionCountyA);
    observer.observe(sectionCountyB);
    observer.observe(sectionDone);
  });
</script>

<main>
  {#if activeOverlay !== "done"}
    <div style=
    "position: fixed; 
    top: 0; 
    left: 0; 
    width: 100%; 
    height: 100vh; 
    z-index: 0;">
      <MapSection {zoomTarget} />
    </div>

    <div style=
    "position: fixed; 
    top: 0; 
    left: 0; 
    width: 100%; 
    height: 100vh; 
    z-index: 2; 
    pointer-events: none;">

      {#if activeOverlay === "state"}
        <div style=
        "position: absolute; 
        bottom: 10%; 
        left: 50%; 
        transform: translateX(-50%);
        background: rgba(255, 255, 255, 0.9); 
        padding: 1rem; 
        border-radius: 1rem; 
        max-width: 400px; 
        text-align: center;">
          
          <p style="margin-top: 0.75rem; font-family: 'Libre Baskerville', serif; font-style: italic; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
            This is New Jersey. It is the most densely populated state in the
            U.S., with a population of 9.5 million people occupying just 8,000
            square miles. And, through some twist of fate, it is the place I
            call home.
          </p>
        </div>
      {:else if activeOverlay === "countyA"}
        <div style=
          "position: absolute; 
          bottom: 10%; 
          left: 50%; 
          transform: translateX(-50%);
          background: rgba(255, 255, 255, 0.9); 
          padding: 1rem; 
          border-radius: 1rem; 
          max-width: 400px; 
          text-align: center;">

          <p style="margin-top: 0.75rem; font-family: 'Libre Baskerville', serif; font-style: italic; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
            This is Hunterdon County. It is one of the wealthiest counties in
            the state, known for its affluent neighborhoods, top-rated
            education, and incredible quality of life.
          </p>
        </div>

        <div style=
          "position: absolute;
          max-width: 350px; 
          background: rgba(255, 255, 255, 0.85);
          padding: 1rem; 
          border-radius: 12px; 
          <!-- box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); -->
          z-index: 10; 
          transition: opacity 0.5s ease, transform 0.5s ease;
          top: 20%; 
          left: 5%;">
          <img src="https://upload.wikimedia.org/wikipedia/commons/d/d5/Clinton_NJ_Easter_2014.jpg" alt="Hunterdon County" style="width: 100%; height: auto; border-radius: 8px;"/>
        </div>
        
      {:else if activeOverlay === "countyB"}
        <div style=
          "position: absolute; 
          bottom: 10%; 
          left: 50%; 
          transform: translateX(-50%);
          box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
          background: rgba(255, 255, 255, 0.9); 
          padding: 1rem; 
          border-radius: 1rem; 
          max-width: 400px; 
          text-align: center;">

          <p style="margin-top: 0.75rem; font-family: 'Libre Baskerville', serif; font-style: italic; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
            And this is Essex County. It is one of the poorest counties in the
            state, with many neighborhoods falling in the high-poverty category.
            Homelessness is prevalent, and infrastructure and
            education fall considerably below the state standard.
          </p>
        </div>

        <div style=
          "position: absolute;
          max-width: 350px; 
          background: black;
          padding: 1rem; 
          border-radius: 12px; 
          background: rgba(255, 255, 255, 0.85);
          box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
          z-index: 10; 
          transition: opacity 0.5s ease, transform 0.5s ease;
          top: 10%; 
          right: 10%;">
          <img src="https://static01.nyt.com/images/2019/11/15/nyregion/00newark8/00newark8-articleLarge.jpg?quality=75&auto=webp&disable=upscale" alt="Essex County" style="width: 100%; height: auto; border-radius: 8px;"/>
        </div>
      {/if}
    </div>
  {/if}

  <div style="position: relative; z-index: 1;">
    <section bind:this={sectionState} style="height: 100vh"></section>
    <section bind:this={sectionCountyA} style="height: 100vh;"></section>
    <section bind:this={sectionCountyB} style="height: 100vh;"></section>
    <section bind:this={sectionDone} style="height: 100vh;">
      <StorySection />
      <ImageSection />
      <SVISection />
      <DataViz /> 
      <FallingWords />
      <Timeline />
      <div bind:this={walkOutTrigger} style="height: 1px;"></div>
      <Animation {phase} />
      <div bind:this={walkBackTrigger} style="height: 1px;"></div>
      <Ending/>
    </section>
  </div>
</main>