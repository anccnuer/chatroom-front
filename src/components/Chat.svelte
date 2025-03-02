<script>
    import FriendList from "./FriendList.svelte";
    import Message from "./Message.svelte";
    const ws = new WebSocket("ws://localhost:3030/ws");

    let myip = '';
    let friends = [
        { name: "公共频道", online: true },
        { name: "李扬天佑", online: false },
        { name: "章鱼红", online: true },
        { name: "外国人", online: false },
        { name: "无名氏", online: true },
    ];

    let messages = $state([
        { nickname: "李扬天佑", content: "系兄弟就来砍我", isMe: false },
        { nickname: "我", content: "道士十五狗，全区横着走", isMe: true },
    ]);

    let textareaValue = $state("");

    function handleInput(event) {
        textareaValue = event.target.value;
    }

    function handleEnter(event) {
        if (event.key === "Enter" && !event.shiftKey) {
            // 当按下 Enter 键且没有 Shift 时发送消息
            event.preventDefault(); // 阻止默认的换行行为
            sendMessage();
        }
    }

    function sendMessage() {
        if (textareaValue.trim()) {
            ws.send(JSON.stringify({ toip: "public", message: textareaValue }));
            textareaValue = "";
        }
    }
    ws.onmessage = (event) => {
        let mes = JSON.parse(event.data);
        if (mes?.type == "online") {
            myip = mes.myip;
        } else {
            messages = [
                ...messages,
                { nickname: mes.fromip, content: mes.message, isMe: (myip == mes.fromip) }, 
            ];
        }
    };
</script>

<div class="chat-main">
    <div class="chat-header">{friends[0].name}</div>
    <div class="chat-body">
        {#each messages as message, index}
            <Message
                content={message.content}
                isMe={message.isMe}
                nickname={message.nickname}
            />
        {/each}
    </div>
    <div class="chat-input">
        <textarea
            oninput={handleInput}
            onkeydown={handleEnter}
            placeholder="可以畅快聊天啦！在此输入……"
            value={textareaValue}
        ></textarea>
        <button onclick={sendMessage}>Send</button>
    </div>
</div>

<div class="friend-list-container">
    <FriendList {friends} />
</div>
