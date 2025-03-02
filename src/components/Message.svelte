<script>
    export let content;
    export let isMe;
    export let nickname;
</script>

<div class="chat-message" class:me={isMe}>
    <div
        class="nickname"
        style="color: {isMe ? '#fff' : '#000'}; background-color: {isMe
            ? '#0084ff'
            : '#e1e1e1'}; width:4.2rem;padding: 5px; border-radius: 15px; margin: 5px;"
    >
        {nickname}
    </div>
    <div
        class="content"
        style="background-color: {isMe ? '#0084ff' : '#e1e1e1'}; color: {isMe
            ? '#fff'
            : '#000'}; padding: 5px; border-radius: 5px;"
    >
        {content}
    </div>
</div>
