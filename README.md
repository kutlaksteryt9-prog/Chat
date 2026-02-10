<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Простой Мессенджер</title>
<style>
  body { font-family: Arial; background: #f0f0f0; padding: 20px; }
  #chat { border: 1px solid #ccc; background: #fff; height: 400px; overflow-y: scroll; padding: 10px; }
  #message { width: 80%; }
  #send { width: 18%; }
  .msg { margin: 5px 0; }
  .user { color: blue; }
  .text { color: black; }
</style>
</head>
<body>

<h2>Простой Мессенджер</h2>
<div id="chat"></div>
<input type="text" id="message" placeholder="Введите сообщение">
<button id="send">Отправить</button>

<script>
  const chat = document.getElementById('chat');
  const messageInput = document.getElementById('message');
  const sendBtn = document.getElementById('send');

  // Загрузка сообщений из localStorage
  let messages = JSON.parse(localStorage.getItem('messages') || '[]');
  function render() {
    chat.innerHTML = '';
    messages.forEach(m => {
      const div = document.createElement('div');
      div.classList.add('msg');
      div.innerHTML = '<span class="user">' + m.user + ':</span> <span class="text">' + m.text + '</span>';
      chat.appendChild(div);
    });
    chat.scrollTop = chat.scrollHeight;
  }
  render();

  sendBtn.onclick = () => {
    const text = messageInput.value.trim();
    if (!text) return;
    messages.push({user: 'Вы', text});
    localStorage.setItem('messages', JSON.stringify(messages));
    messageInput.value = '';
    render();
  }

  // Отправка по Enter
  messageInput.addEventListener('keydown', e => {
    if (e.key === 'Enter') sendBtn.onclick();
  });
</script>

</body>
</html>
