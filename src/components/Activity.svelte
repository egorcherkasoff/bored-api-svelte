<script>
    export let activity;
    export let accessibility;
    export let type;
    export let participants;
    export let price;
    export let link;
</script>

<article>
    <h2>Try to {activity}</h2>
    <p>Participants: {participants}</p>
    <p>Accessibility: {accessibility}</p>
    <p>Type: {type}</p>
    <p>Price: {price}</p>
    {#if link}
        <a href={link}>Link: {link}</a>
    {/if}
</article>

<style lang="scss">
    article {
        padding: 10px;
        margin-top: 15px;
        border-radius: 5px;
        border: 1px solid #d4adfc;
        background-color: #0c134f;
    }
    p {
      margin-top: 5px;
    }
</style>
