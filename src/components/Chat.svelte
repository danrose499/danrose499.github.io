<script>
  import { onMount } from 'svelte';
  import chatIcon from '../assets/images/icons/chat.png';
  
  // Check if the API is available
  async function checkApiAvailability() {
    try {
      const response = await fetch(API_ENDPOINT, {
        method: 'OPTIONS',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json',
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type'
        }
      });
      
      // If we get any response, the endpoint is reachable
      isApiAvailable = true;
      return true;
    } catch (error) {
      console.warn('API availability check failed:', error);
      isApiAvailable = false;
      return false;
    }
  }
  
  // Check API availability on component mount
  onMount(() => {
    checkApiAvailability();
  });

  let isOpen = false;
  let input = '';
  let loading = false;
  let error = '';
  let messages = [];

  // API endpoint configuration
  const API_ENDPOINT = 'https://openai-proxy.danielrosenthal.workers.dev';
  let isApiAvailable = false; // Start as false until we confirm API is available

  function toggleChat() {
    isOpen = !isOpen;
    if (isOpen && messages.length === 0) {
      messages = [{ role: 'assistant', content: 'Ask me anything about my experience, projects, or skills!' }];
      
      // Check API availability when chat is first opened
      if (isApiAvailable) {
        checkApiAvailability();
      }
    }
  }

  async function sendMessage() {
    const text = input.trim();
    if (!text || loading) return;
    
    error = '';
    input = '';
    messages = [...messages, { role: 'user', content: text }];
    loading = true;
    
    try {
      if (!isApiAvailable) {
        throw new Error('Chat API is currently unavailable');
      }

      const response = await fetch(API_ENDPOINT, {
        method: 'POST',
        mode: 'cors',
        headers: { 
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        },
        body: JSON.stringify({ 
          messages: [{ 
            role: 'user', 
            content: text 
          }] 
        })
      });
      
      if (!response.ok) {
        const errorText = await response.text();
        console.error('API Error:', { status: response.status, statusText: response.statusText, errorText });
        throw new Error(`API request failed with status ${response.status}`);
      }
      
      const data = await response.json();
      const assistant = data?.choices?.[0]?.message?.content?.trim?.();
      
      if (!assistant) {
        throw new Error('No content in API response');
      }
      
      messages = [...messages, { role: 'assistant', content: assistant }];
    } catch (err) {
      console.error('Chat error:', err);
      isApiAvailable = false;
      error = 'The chat feature is currently unavailable. Please try again later.';
      // Add a helpful message to the chat
      messages = [...messages, { 
        role: 'assistant', 
        content: 'I\'m sorry, but the chat feature is currently unavailable. Please try again later or contact me through other means.'
      }];
    } finally {
      loading = false;
    }
  }

  function handleKeyDown(e) {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      sendMessage();
    }
  }
</script>

<div class="chat-container">
  {#if isOpen}
    <div class="chat-window">
      <div class="chat-header">
        <h3>Chat with me</h3>
        <button class="close-btn" on:click={toggleChat} aria-label="Close chat">
          &times;
        </button>
      </div>
      <div class="messages">
        {#each messages as message, i (i)}
          <div class="message {message.role}">
            {message.content}
          </div>
        {/each}
        {#if loading}
          <div class="message assistant">
            <div class="typing-indicator">
              <span></span><span></span><span></span>
            </div>
          </div>
        {/if}
      </div>
      <div class="input-area">
        <textarea
          bind:value={input}
          on:keydown={handleKeyDown}
          placeholder="Type your message..."
          rows="1"
          disabled={loading}
        ></textarea>
        <button on:click={sendMessage} disabled={loading || !input.trim()}>
          Send
        </button>
      </div>
      {#if error}
        <div class="error">{error}</div>
      {/if}
    </div>
  {/if}
  
  <button class="chat-button" on:click={toggleChat} aria-label="Open chat">
    <img src={chatIcon} alt="Chat" width="24" height="24" />
  </button>
</div>

<style>
  .chat-container {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
  }

  .chat-button {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: #4a90e2;
    border: none;
    color: white;
    cursor: pointer;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.2s, box-shadow 0.2s;
  }

  .chat-button:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  }

  .chat-button:active {
    transform: scale(0.98);
  }

  .chat-window {
    position: absolute;
    bottom: 70px;
    right: 0;
    width: 320px;
    max-width: 90vw;
    height: 400px;
    background: white;
    border-radius: 12px;
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.15);
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .chat-header {
    padding: 12px 16px;
    background: #4a90e2;
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .chat-header h3 {
    margin: 0;
    font-size: 1rem;
  }

  .close-btn {
    background: none;
    border: none;
    color: white;
    font-size: 1.5rem;
    cursor: pointer;
    line-height: 1;
    padding: 0 4px;
  }

  .messages {
    flex: 1;
    overflow-y: auto;
    padding: 12px;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .message {
    max-width: 80%;
    padding: 8px 12px;
    border-radius: 18px;
    line-height: 1.4;
    word-wrap: break-word;
  }

  .message.user {
    align-self: flex-end;
    background: #4a90e2;
    color: white;
    border-bottom-right-radius: 4px;
  }

  .message.assistant {
    align-self: flex-start;
    background: #f0f0f0;
    color: #333;
    border-bottom-left-radius: 4px;
  }

  .input-area {
    display: flex;
    padding: 12px;
    border-top: 1px solid #eee;
    gap: 8px;
  }

  textarea {
    flex: 1;
    border: 1px solid #ddd;
    border-radius: 20px;
    padding: 8px 12px;
    resize: none;
    font-family: inherit;
    font-size: 0.9rem;
    max-height: 100px;
  }

  textarea:focus {
    outline: none;
    border-color: #4a90e2;
  }

  button {
    padding: 8px 16px;
    background: #4a90e2;
    color: white;
    border: none;
    border-radius: 20px;
    cursor: pointer;
    transition: background 0.2s;
  }

  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }

  .error {
    color: #e74c3c;
    font-size: 0.8rem;
    padding: 0 12px 8px;
    text-align: center;
  }

  .typing-indicator {
    display: flex;
    gap: 4px;
    padding: 8px 0;
  }

  .typing-indicator span {
    width: 8px;
    height: 8px;
    background: #999;
    border-radius: 50%;
    display: inline-block;
    animation: typing 1.4s infinite ease-in-out;
  }

  .typing-indicator span:nth-child(1) { animation-delay: 0s; }
  .typing-indicator span:nth-child(2) { animation-delay: 0.2s; }
  .typing-indicator span:nth-child(3) { animation-delay: 0.4s; }

  @keyframes typing {
    0%, 60%, 100% { transform: translateY(0); }
    30% { transform: translateY(-4px); }
  }
</style>
