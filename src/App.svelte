<script>
    let selected_activity = "";
    import Activity from "./components/Activity.svelte";
    const base_url = "http://www.boredapi.com/api/activity/";
    const activities = [
        "education",
        "recreational",
        "social",
        "diy",
        "charity",
        "cooking",
        "relaxation",
        "music",
        "busywork",
    ];
    let repeat = false;
    let promise;

    function handleClick() {
        repeat = true;
        promise = GetActivities();
    }

    async function GetActivities() {
        let url = "";
        if (selected_activity !== "") {
            url = `${base_url}?type=${selected_activity}`;
        } else {
            url = base_url;
        }
        const response = await fetch(url);
        const data = await response.json();
        if (data.error) {
          throw new Error(data.error)
        }
        return data;
    }
</script>

<main>
    <h1>Bored?</h1>
    <p>
        Select what you'd like to do and click the button! (Or leave it blank,
        if you want to get random stuff)
    </p>
    <select name="activities" id="activities" bind:value={selected_activity}>
        <option value="">Select activity here...</option>
        {#each activities as activity}
            <option value={activity}>{activity}</option>
        {/each}
    </select>
    {#if repeat}
        <button on:click={handleClick}>TRY AGAIN</button>
    {:else}
        <button on:click={handleClick}>I'M BORED</button>
    {/if}
    {#if promise !== undefined}
        {#await promise}
            Thinking how to keep you busy...
        {:then data}
            <Activity {...data} />
        {:catch err}
            <p>Something went wrong! ({err})</p> 
        {/await}
    {/if}
</main>

<style lang="scss">
    h1,
    p {
        text-align: center;
        word-spacing: 2px;
        letter-spacing: 0.7px;
    }
    h1 {
        font-size: 2em;
        margin-bottom: 15px;
    }
    p {
        font-size: 1.1em;
        margin-bottom: 5px;
    }
    main {
        background-color: #1d267d;
        padding: 25px;
        border-radius: 30px;
    }
    select {
        font-size: 1em;
        margin-top: 15px;
        display: block;
        padding: 10px;
        border-radius: 5px;
        color: #d4adfc;
        background-color: #0c134f;
        border: 1px solid #d4adfc;
        width: 100%;
        text-transform: capitalize;
        cursor: pointer;
        outline: none;
    }
    button {
        font-size: 1em;
        margin-top: 15px;
        display: block;
        padding: 10px;
        border-radius: 5px;
        color: #d4adfc;
        background-color: #0c134f;
        border: 1px solid #d4adfc;
        width: 100%;
        font-weight: bold;
        cursor: pointer;
        outline: none;
        letter-spacing: 1px;
        &:active {
            background-color: #1d267d;
        }
    }
</style>
