<script>
    export let name;
    export let online;

    function handleClick() {
        // 切换聊天对象逻辑
        console.log(`Selected friend: ${name}`);
    }
</script>


<button class="friend" on:click={handleClick}>
    <div class="avatar" style="background-color: {online ? '#3d84a8' : '#ff2e63'};">{online ? '在线' : '离线'}</div>
    <div class="name">{name}</div>
  </button>