<script>
    import Character from "../components/character.svelte";
    let x = $state(0);
    let y = $state(0)
</script>

<svelte:window on:mousemove={(e) => {
    x = e.x;
    y = e.y;
}}></svelte:window>
<Character bind:x bind:y />