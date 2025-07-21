<!-- Initial code w/ slight modifications to fit the website theme -->
<script>
    let { children } = $props();
</script>

<div class="article-text">
    <p>
        {@render children()}
    </p>
</div>

<style>
    .article-text {
        margin: 50vh auto;
        width: 50%;
        background-color: white;
        color: black;
        border: rgba(0, 0, 0, 0);
        border-radius: 20px;
        padding: 20px;
        font-family: "EB Garamond", serif;
        font-size: 1.3rem;
        text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.3);
        line-height: 1.2;
    }
</style>
