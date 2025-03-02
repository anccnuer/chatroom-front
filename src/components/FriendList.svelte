<script>
    export let friends;
    import Friend from "./Friend.svelte"
</script>

<div class="friend-list">
    {#each friends as friend}
        <Friend name={friend.name} online={friend.online} />
    {/each}
</div>
