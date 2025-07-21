<script>
    import * as Highcharts from "highcharts";
    import { Chart } from "@highcharts/svelte";
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";
    import { onMount } from "svelte";

    let chartVisible = { svi: false, blackPops: false, blackIncome: false, blackHousing: false }; 
    let sviRef, popsRef, incomeRef, housingRef; 
    const observerOptions = { threshold: 0.4 }; 

    // I used ChatGPT to understand the logic of animating the charts with every scroll. 
    function setupObserver(ref, key){
        const observer = new IntersectionObserver(([entry]) => {
            if(entry.isIntersecting) chartVisible[key] = true; 
        }, observerOptions); 
        observer.observe(ref);
    }

    onMount(() => {
        setupObserver(sviRef, "svi");
        setupObserver(popsRef, "blackPops");
        setupObserver(incomeRef, "blackIncome");
        setupObserver(housingRef, "blackHousing");
    });


    const SVIOptions = {
        chart: { type: "column" }, 
        title: { text : "Social Vulnerability Index", 
            style: { fontSize: "20px", fontFamily: "Frank Ruhl Libre, serif" }
         }, 
        yAxis: { max: 1, title: { text: "SVI Value", style: { fontSize: "15px", fontFamily: "EB Garamond, serif" } }, 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            } 
        }, 
        xAxis: { categories: ["Essex County", "Hunterdon County"], 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            }
        }, 
        series: [{ 
            name: 'SVI Index', style: { fontFamily: "EB Garamond, serif", fontSize: "14px" },
            color: '#000000',
            data: [
                { y: 0.94, color: '#000000', name: 'Essex'}, 
                { y: 0.04, color: '#888888', name: 'Hunterdon'}, 
            ], 
            animation: { duration: 800 }
        }]
    }; 

    const blackPops = {
        chart: { type: "column" }, 
        title: { text : "% Black Population",
            style: { fontSize: "20px", fontFamily: "Frank Ruhl Libre, serif" }, 
         }, 
        yAxis: { max: 100, title: { text: "% Black Population", style: { fontSize: "15px", fontFamily: "EB Garamond, serif" } }, 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            }  
        }, 
        xAxis: { categories: ["Essex", "Hunterdon"], 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            } 
        }, 
        series: [{
            name: '% Black Population', style: { fontFamily: "EB Garamond, serif", fontSize: "14px" },
            color: '#000000',
            data: [
                { y: 36.9, color: '#000000' },
                { y: 2.6, color: '#888888' },
            ], 
            animation: { duration: 800 }
        }]
    }; 

    const blackIncome = {
        chart: { type: "column" },
        title: { text : "Black Median Income", 
            style: { fontSize: "20px", fontFamily: "Frank Ruhl Libre, serif" }, 
        },
        yAxis: { max: 150000, title: { text: "Black Median Income", style: { fontSize: "15px", fontFamily: "EB Garamond, serif" } },
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            }  
         }, 
         xAxis: { categories: ["Essex", "Hunterdon"], 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            } 
        }, 
        series: [{
            name: 'Black Median Income', style: { fontFamily: "EB Garamond, serif", fontSize: "14px" },
            color: '#000000',
            data: [
                { y: 56411, color: '#000000' },
                { y: 121838, color: '#888888' }
            ], 
            animation: { duration: 800 }
        }]
    };
 
    
    const blackHousing = {
        chart: { type: "column" }, 
        title: { text : "% Black Owner-Occupied Housing", 
            style: { fontSize: "20px", fontFamily: "Frank Ruhl Libre, serif" }, 
         }, 
        yAxis: { max: 100, title: { text: "% Black Owner-Occupied Housing", style: { fontSize: "15px", fontFamily: "EB Garamond, serif" } },
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            }  
        }, 
        xAxis: { categories: ["Essex", "Hunterdon"], 
            labels: {
                style: { fontFamily: "EB Garamond, serif", fontSize: "14px" }
            } 
        }, 
        series: [{
            name: '% Black Owner-Occupied Housing', style: { fontFamily: "EB Garamond, serif", fontSize: "14px" },
            color: '#000000',
            data: [
                { y: 24.1, color: '#000000' },
                { y: 1.3, color: '#888888' }
            ], 
            animation: { duration: 800 }
        }]
    };

</script>

<div>
    <Scroller layout="left">
        {#snippet sticky()} 
            <div class="small-multiples">
                <div bind:this={sviRef}>
                    {#if chartVisible.svi}
                    <Chart highcharts={Highcharts} options={SVIOptions} />
                    {/if}
                </div>
            </div>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                The following data is directly taken from the Black Wealth Data Center. 
                When comparing the SVI of both counties, it is clear that Essex County has an incredibly high 
                value of 0.94. However, Hunterdon County's value is a mere 0.04... the <strong>lowest</strong>
                value in the state. 
                <br/><br/>
                This massive disparity cannot be chalked up to a coincidence. 
            </ArticleText>
        {/snippet}
    </Scroller>

    <Scroller layout="left">
        {#snippet sticky()} 
            <div class="small-multiples">
                <div bind:this={popsRef}></div>
                {#if chartVisible.blackPops}
                <Chart highcharts={Highcharts} options={blackPops} />
                {/if}
            </div>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                When we look at the Black population in each county, it is significant 
                that the percentage in Essex County, 36.9%, is <strong>much higher</strong> than that of 
                Hunterdon County, or 2.6%. There is a clear connection between social vulnerability and the amount of 
                Black residents in a county. 
            </ArticleText>
        {/snippet}
    </Scroller>

    <Scroller layout="left">
        {#snippet sticky()} 
            <div class="small-multiples">
                <div bind:this={incomeRef}></div>
                {#if chartVisible.blackIncome}
                <Chart highcharts={Highcharts} options={blackIncome} />
                {/if}
            </div>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                This data examines the difference between Black median income in both counties, which can help to clearly 
                indicate financial capacity. Essex County's Black median income falls at a mere <strong>$56,411,</strong> whereas Hunterdon County's 
                is <strong>more than double that</strong> at $121,838.
                <br/><br/>
                Persistent wealth inequality and systemic discrimination in relation to housing, healthcare, and education
                have left Black households and individuals <strong>disproportionately vulnerable to poverty.</strong> In today's world, low financial standing 
                directly translates to a lack of security and safety in the face of disasters and disruptive global events. 
                <br/><br/>
                With the median household income in New Jersey
                reaching a whopping $101,050, Black residents of Essex County are at a significant disadvantage in 
                hazardous situations. 
            </ArticleText>
        {/snippet}
    </Scroller>

    <Scroller layout="left">
    {#snippet sticky()} 
            <div class="small-multiples">
                <div bind:this={housingRef}></div>
                {#if chartVisible.blackHousing}
                <Chart highcharts={Highcharts} options={blackHousing} />
                {/if}
            </div>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                This relationship is also apparent when looking at the percentage of Black-owner occupied homes in both counties. 
                There is a 24.1% Black home ownership rate in Essex County, as opposed to a 1.3% ownership rate in Hunterdon County. 
                This corresponds to the data given about the Black populations in both counties, as Essex County showed a significantly 
                higher percentage. 
                <br/><br/>
                These staggering differences are made clearer when realizing that Hunterdon County is a 
                <strong>predominantly white town,</strong> with a non-Hispanic white population percentage of 81.1%. 
                <br/><br/>
                More importantly, however, one thing in relation to this tale of two counties has become 
                increasingly apparent. 
            </ArticleText>
        {/snippet}
    </Scroller>

</div>

<style>
    .small-multiples {
        display: flex; 
        flex-wrap: wrap; 
        gap: 2rem; 
        justify-content: center;
    }

</style>

