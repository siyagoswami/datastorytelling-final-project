<script>
    import ImagePanel from '../lib/ImagePanel.svelte';
    import TextPanel from '../lib/TextPanel.svelte';

let currentStep = 0; 
const images = [
    'https://jerseybee.org/wp-content/uploads/2024/06/FeaturedImage_SegregationIntro_June2024-1-2048x1152.jpg',
    'https://jerseybee.org/wp-content/uploads/2024/06/Map_Redlining1939_June2024-1844x2048.jpg',
    'https://www.njspotlightnews.org/wp-content/uploads/sites/123/2022/03/Attendees-at-school-desegregation-rally-Trenton-March-31-2022.jpg',
    'https://whyy.org/wp-content/uploads/2021/01/camden_NJ_illegal_dumping_011121_01-768x588.jpg',
]; 

</script>
<!-- I used ChatGPT to understand how the 'currentStep' mechanism would trigger the text and corresponding image. -->
<!-- Source: https://jerseybee.org/2024/06/24/in-essex-county-new-jerseys-history-of-segregation-persists/ -->
<div class="scrolly-container">
    <div class="text-column">
        <TextPanel on:enter={() => (currentStep = 0)}>
            <p style="line-height: 1.2; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
                The photo above is an aerial view of Newark, New Jersey during the 1960s-1970s. 
                As the largest municipality in Essex County, it serves as a blueprint for understanding
                the area's massive inequality and discrimination. 
                <br/><br/>
                Essex County is one of the foremost examples of New Jersey's slave history. 
                From street names to historical structures, there are remnants of the
                atrocities are omnipresent.
                Bloomfield, a township in the county, was home to Lieutenent Colonel Thomas Cadmus. 
                Although he is primarily remembered as an officer in the American Revolutionary War, his former residence is a 
                stark reminder that he was a slave-owner. <strong>He enslaved almost 4,700 Black people 
                in the mid-eighteenth century.</strong>
                <br/><br/>
                Cadmus was not the only slave-owner in the area. New Jersey was 
                actually even referred to as the "slave state of the North" because 
                it enslaved <strong>more than two-thirds of all slaves in the North by the 1830s.</strong>
            </p>
        </TextPanel>

        <TextPanel on:enter={() => (currentStep = 1)}>
            <!-- Source: https://jerseybee.org/2024/06/24/in-essex-county-new-jerseys-history-of-segregation-persists/ -->
            <p style="line-height: 1.2; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
                Almost a century after slavery was outlawed, the federal government 
                continued to engage in discriminatory practices—especially in regards to housing. 
                Known more generally as red-lining, the Federal Housing Administration (FHA)
                drew red lines around Black neighborhoods and considered those areas 
                as investment risks. <strong>As a result, Black households were denied mortgages and bank services, 
                stunting any potential socioeconomic mobility.</strong> 
                <br/><br/>
                Some neighborhoods in Newark were explicitly called slum sections and designated specifically for lower-income people. 
                Discriminatory attitudes by predominantly white bankers almost immediately 
                cast away those areas as <strong>'deteriorating' and 'of no use'</strong> due to the increasing number 
                of Black families. On this 1939 map, Newark and Bloomfield were labeled
                red and 'Fourth Grade,' whereas predominantly white areas such as Maplewood and Upper
                Montclair were green and 'First Grade.'<strong>All investments ultimately prioritized and/or went to 'First Grade' communities.</strong>
                <br/><br/>
                And, almost a century after that, racial discrimination in housing persists. 
                In 2022, New Jersey's Lakeland Bank was fined $13 million because it was accused 
                of avoiding giving mortgages to and opening branches in Black and Latinx communities.
                <strong>And, according to the New Jersey Institute for Social Justice,
                Black and Latinx households in the county are three times more likely to be impoverished 
                and half as likely to own property or a home compared to white households.</strong> 
            
            </p>
        </TextPanel>

        <TextPanel on:enter={() => (currentStep = 2)}>
             <p style="line-height: 1.2; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
                <!-- Source: https://jerseybee.org/2024/06/24/in-essex-county-new-jerseys-history-of-segregation-persists/ -->
                The inequality unfortunately does not stop there. According to the New Jersey Department of Health, 
                Black individuals are also less likely to have health insurance.
                This is a significant challenge because they are also more vulnerable to environmental factors and stressors 
                like mold, toxins from sanitary landfills, and air pollutants from waste facilities. A fourth power plant 
                was just recently approved in the impoverished Ironbound neighborhood in Newark, despite much opposition 
                from a community already struggling from high asthma rates. This continued exposure can ultimately lead 
                to <strong>preventable death.</strong>
                <br/><br/>
                Furthermore, predominantly Black low-income communities were shown to have faced 
                neglect from federal assistance programs after Hurricane Sandy, the most
                destructive hurricane to ever be experienced by the state, in 2015. 
                <br/><br/> 
                <!-- Source: https://www.njspotlightnews.org/2022/05/newark-schools-segregation-nearby-communities-stark-black-white-divide/ -->
                Education also remains heavily segregated. Newark has some of the most highly-segregated
                schools in the country, ranking first in economic segregation and second in racial segregation.
                For context, 75% of students in the Glen Ridge school district of the county are white, 
                yet in the East Orange school district, white students make up a stark 1%. 
                <br/><br/>
                <strong>And the distance between the two districts? Just 3 miles. </strong>
            </p>
        </TextPanel>

        <TextPanel on:enter={() => (currentStep = 3)}>
            <p style="line-height: 1.2; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);">
                All of these factors combined lead to what is known as <strong>social vulnerability.</strong>
                <br/><br/>
                <!-- Source: https://www.atsdr.cdc.gov/place-health/php/svi/index.html -->
                Social vulnerability describes demographic and socioeconomic stressors like poverty, lack of 
                access to transportation, and crowded housing, and their capacity to <strong>negatively affect</strong> communities 
                during hazardous or threatening periods. These hazards can either be natural disasters, human-caused disasters, 
                or disease outbreaks. 
                <br/><br/>
                The Social Vulnerability Index (SVI) is a metric that assesses 
                <strong>a community's capacity and ability to overcome these challenges through its socioeconomic aspects.</strong>
                Assessed on a scale of 0 to 1, a <strong>higher score indicates greater social vulnerability.</strong>
                For example, a low-income neighborhood with crowded housing would likely spread a contagious disease 
                more rapidly, yet its inhabitants may not have health insurance for the vaccination. Or, a neighborhood with 
                weak infrastructure and a lack of access to transportation may suffer disproportionately from a tornado 
                because the structural integrity of each home is heavily compromised and its residents do not have the 
                ability to evacuate. Thus, social vulnerability points to a <strong>clear relationship</strong> between socioeconomic factors 
                and the extent of suffering caused by an event. 
                <br/><br/>
                Social vulnerability and the SVI are of the utmost importance to consider as we grapple with the facts 
                of an ever-evolving world. Climate change is happening right before us. Air and water pollution remain 
                prevalent threats to a healthy and sustainable world. And the gap between the wealthy and the poor is only rising.
                <br/><br/>
                Let's take a look at some data to put all these words into context. 
            </p>
        </TextPanel>
    </div>

    <ImagePanel {images} {currentStep}/>
</div>

<style>
    .scrolly-container {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

    .text-column {
        padding: 0;
    }

    @media (max-width: 768px) {
        .scrolly-container {
            display: block;
        }
    }
</style>