<script context="module" lang="ts">
    var bugUrl = "/#bug.html";

	export async function load({ fetch })
	{
        var bugFetch = await fetch(bugUrl);

		return {
            props: 
            {
                bug: await bugFetch.text()
            }
        };
	}
</script>

<script>
    export var bug;
    export var bugBrowser;

    async function loadBrowser()
    {
        var bugFetch = await fetch(bugUrl);
        bugBrowser = await bugFetch.text();
    }

    loadBrowser();
</script>

<style>
    code
    {
        color: darkred;
    }

    .result-container
    {
        padding: 1rem;
        background: rgba(0, 0, 0, 0.05);
    }
</style>

<h1>Svelte Kit's <code>fetch</code> and the Browser's <code>fetch</code> Produce Inconsistent Results</h1>

<br>
<br>
<br>

<h2>Result of <code>await fetch({bugUrl})</code> when called from Svelte <code>load</code></h2>
<div class="result-container">{@html bug}</div>
<h3>Verdict: Svelte does successfully retrieve the file</h3>

<br>
<br>
<br>

<h2>Result of <code>await fetch({bugUrl})</code> when called from the browser</h2>
<div class="result-container">{@html bugBrowser}</div>
<h3>Verdict: The browser does not successfully retrieve the file (and instead retrieves src/routes/index.svelte and duplicates the content)</h3>
