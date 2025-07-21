<script>
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";
</script>

    <div>
    <Scroller layout="right">
        {#snippet sticky()}
            <h1 style="font-family: Libre Baskerville, serif; font-style: italic; text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.4);">
                1 state. 2 different counties. 2 vastly different realities.
            </h1>
            <p style="font-family: Libre Baskerville, serif; font-style: italic; font-size: 1rem; padding: 0.5rem; line-height: 1.4;">
                Now comes the question of... why? 
                Why are these counties, separated geographically only by a mere 50 miles and 2 inter-state routes, 
                so vastly different in practically every single aspect? How can there be such vast inequality in the span of a one-hour drive? 
            </p>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                But doesn't wealth-related inequality exist everywhere? It is a virtually inescapable part of life, 
                and you will find socioeconomic division no matter where you go. 
                <br/><br/>
                <strong>In other words... what makes these two counties so special? </strong>
            </ArticleText>

            <ArticleText>
                Well, that is true. Unfortunately, many people have no choice but to grapple with the consequences of wealth-related inequality reflected in their own lives.
                <br/><br/>
                What makes these two counties so special, however, is the fact that they clearly show <strong>what the disparities are based on.</strong>
            </ArticleText>

            <ArticleText>
                But hold off on any final guesses. The picture might look a little fuzzy right now, 
                but there are a couple of more things that must be understood. 
                <br/><br/>
                To understand the why and the what, we need to look at the <i>how</i>. <strong>And that requires turning some pages back in history.</strong>
            </ArticleText>
        {/snippet}
    </Scroller>
</div>

