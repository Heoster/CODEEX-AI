
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heoster's Wikinet AI - Your Knowledge Assistant</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #2563eb;
      --secondary-color: #1d4ed8;
      --accent-color: #3b82f6;
      --text-color: #1f2937;
      --light-text: #6b7280;
      --bg-color: #f9fafb;
      --chat-bg: #ffffff;
      --user-msg: #dbeafe;
      --bot-msg: #f3f4f6;
      --wiki-msg: #f8fafc;
      --saffron: #ff9933;
      --white: #ffffff;
      --green: #138808;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
      background: var(--bg-color);
      color: var(--text-color);
      display: flex;
      flex-direction: column;
      min-height: 100vh;
      margin: 0;
      padding: 0;
      line-height: 1.6;
    }

    .app-container {
      display: flex;
      flex-direction: column;
      flex: 1;
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
      padding: 20px;
    }

    .chat-container {
      background: var(--chat-bg);
      border-radius: 16px;
      box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
      overflow: hidden;
      display: flex;
      flex-direction: column;
      flex: 1;
      height: calc(100vh - 180px);
      min-height: 500px;
      width: 100%;
      border: 1px solid #e5e7eb;
    }

    .chat-header {
      background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
      color: white;
      padding: 18px 25px;
      font-size: 1.3rem;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 15px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }

    .chat-header img {
      width: 36px;
      height: 36px;
      filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
    }

    .chat-box {
      padding: 25px;
      flex: 1;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      gap: 20px;
      background-color: var(--bg-color);
      background-image: radial-gradient(rgba(0, 0, 0, 0.05) 1px, transparent 1px);
      background-size: 20px 20px;
    }

    .input-area {
      display: flex;
      border-top: 1px solid #e5e7eb;
      padding: 18px;
      background: white;
      box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.02);
    }

    .input-area input {
      flex: 1;
      padding: 14px 22px;
      border: 2px solid #e5e7eb;
      border-radius: 30px;
      outline: none;
      font-size: 1rem;
      transition: all 0.3s;
      background-color: #f9fafb;
      font-family: inherit;
    }

    .input-area input:focus {
      border-color: var(--primary-color);
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
      background-color: white;
    }

    .input-area button {
      margin-left: 15px;
      padding: 0 28px;
      background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-weight: 600;
      font-size: 1rem;
      transition: all 0.2s;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }

    .input-area button:hover {
      opacity: 0.95;
      transform: translateY(-1px);
      box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    }

    .input-area button:active {
      transform: translateY(0);
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }

    .user-message {
      align-self: flex-end;
      background: linear-gradient(135deg, var(--user-msg) 0%, #bfdbfe 100%);
      padding: 14px 20px;
      border-radius: 20px 20px 0 20px;
      max-width: 85%;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
      position: relative;
      border: 1px solid rgba(191, 219, 254, 0.5);
    }

    .bot-message {
      align-self: flex-start;
      background: linear-gradient(135deg, var(--bot-msg) 0%, #e5e7eb 100%);
      padding: 14px 20px;
      border-radius: 20px 20px 20px 0;
      max-width: 85%;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
      position: relative;
      border: 1px solid rgba(229, 231, 235, 0.5);
    }

    .wikipedia-message {
      align-self: flex-start;
      background: linear-gradient(135deg, var(--wiki-msg) 0%, #f1f5f9 100%);
      padding: 18px;
      border-radius: 20px 20px 20px 0;
      max-width: 85%;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
      border-left: 5px solid var(--primary-color);
      border: 1px solid rgba(241, 245, 249, 0.5);
    }

    .typing-indicator {
      display: flex;
      align-self: flex-start;
      padding: 14px 20px;
      background-color: #f3f4f6;
      border-radius: 20px 20px 20px 0;
      width: fit-content;
      gap: 8px;
    }

    .typing-dot {
      width: 10px;
      height: 10px;
      background-color: #6b7280;
      border-radius: 50%;
      animation: typingAnimation 1.4s infinite ease-in-out;
    }

    .typing-dot:nth-child(1) {
      animation-delay: 0s;
    }

    .typing-dot:nth-child(2) {
      animation-delay: 0.2s;
    }

    .typing-dot:nth-child(3) {
      animation-delay: 0.4s;
    }

    @keyframes typingAnimation {
      0%, 60%, 100% { transform: translateY(0); }
      30% { transform: translateY(-5px); }
    }

    .message-time {
      font-size: 0.75rem;
      color: var(--light-text);
      margin-top: 10px;
      text-align: right;
    }

    .info-message {
      align-self: center;
      background-color: #eff6ff;
      padding: 12px 20px;
      border-radius: 20px;
      font-size: 0.9rem;
      color: var(--primary-color);
      margin: 10px 0;
      text-align: center;
      border: 1px solid rgba(219, 234, 254, 0.5);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    }

    .suggestions {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      margin-top: 20px;
      margin-bottom: 15px;
    }

    .suggestion-chip {
      background-color: #eff6ff;
      color: var(--primary-color);
      padding: 10px 18px;
      border-radius: 24px;
      font-size: 0.9rem;
      cursor: pointer;
      transition: all 0.2s;
      border: 1px solid rgba(191, 219, 254, 0.5);
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
    }

    .suggestion-chip:hover {
      background-color: #dbeafe;
      transform: translateY(-2px);
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }

    .wikipedia-link {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      margin-top: 12px;
      color: var(--primary-color);
      text-decoration: none;
      font-weight: 600;
      transition: all 0.2s;
      padding: 6px 12px;
      border-radius: 6px;
      background-color: rgba(59, 130, 246, 0.1);
    }

    .wikipedia-link:hover {
      text-decoration: underline;
      color: var(--secondary-color);
      background-color: rgba(59, 130, 246, 0.2);
    }

    .wikipedia-title {
      font-weight: 700;
      color: var(--primary-color);
      margin-bottom: 10px;
      font-size: 1.2rem;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .wikipedia-title i {
      font-size: 1.1em;
    }

    footer {
      background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
      color: white;
      padding: 25px;
      text-align: center;
      margin-top: 25px;
      border-radius: 0 0 16px 16px;
      box-shadow: 0 -4px 6px -1px rgba(0, 0, 0, 0.1);
    }

    .social-links {
      display: flex;
      justify-content: center;
      gap: 25px;
      margin-top: 20px;
    }

    .social-links a {
      color: white;
      font-size: 1.6rem;
      transition: all 0.3s;
      text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .social-links a:hover {
      color: var(--accent-color);
      transform: translateY(-3px) scale(1.1);
      text-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }

    .footer-text {
      margin-top: 15px;
      font-size: 0.9rem;
      opacity: 0.9;
    }

    .made-in-india {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 8px;
      margin-top: 15px;
      font-size: 1.1rem;
      font-weight: 700;
    }

    .saffron {
      color: var(--saffron);
    }

    .white {
      color: var(--white);
    }

    .green {
      color: var(--green);
    }

    /* Animation for messages */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .user-message, .bot-message, .wikipedia-message, .info-message {
      animation: fadeIn 0.3s ease-out;
    }

    /* Scrollbar styling */
    ::-webkit-scrollbar {
      width: 8px;
    }

    ::-webkit-scrollbar-track {
      background: #f1f1f1;
      border-radius: 10px;
    }

    ::-webkit-scrollbar-thumb {
      background: #c1c1c1;
      border-radius: 10px;
    }

    ::-webkit-scrollbar-thumb:hover {
      background: #a8a8a8;
    }

    /* Responsive adjustments */
    @media (max-width: 1200px) {
      .app-container {
        padding: 18px;
      }
    }

    @media (max-width: 768px) {
      .chat-container {
        height: calc(100vh - 160px);
        border-radius: 14px;
      }
      
      .chat-header {
        padding: 16px 20px;
        font-size: 1.2rem;
      }
      
      .chat-box {
        padding: 20px;
      }
      
      .input-area input {
        padding: 12px 18px;
      }
      
      .input-area button {
        padding: 0 22px;
      }

      .social-links {
        gap: 20px;
      }
    }

    @media (max-width: 480px) {
      .app-container {
        padding: 12px;
      }
      
      .chat-container {
        height: calc(100vh - 140px);
        min-height: 400px;
        border-radius: 12px;
      }
      
      .chat-header {
        padding: 14px 16px;
        font-size: 1.1rem;
      }
      
      .chat-box {
        padding: 16px;
      }
      
      .user-message, .bot-message, .wikipedia-message {
        max-width: 90%;
        padding: 12px 16px;
      }
      
      .input-area {
        padding: 14px;
      }
      
      .input-area input {
        padding: 10px 16px;
      }
      
      .social-links {
        gap: 16px;
      }
      
      .social-links a {
        font-size: 1.4rem;
      }

      .made-in-india {
        font-size: 1rem;
      }
    }
  </style>
</head>
<body>
  <div class="app-container">
    <div class="chat-container">
      <div class="chat-header">
        <img src="https://cdn-icons-png.flaticon.com/512/4712/4712035.png" alt="Chatbot">
      Heoster's Wikinet AI - Your Knowledge Assistant
      </div>
      <div id="chatbox" class="chat-box"></div>
      <div class="input-area">
        <input type="text" id="userInput" placeholder="Ask me anything about any topic..." autocomplete="off" />
        <button onclick="sendMessage()">
          <i class="fas fa-paper-plane"></i> Send
        </button>
      </div>
    </div>
    
    <footer>
      <div>Connect with us</div>
      <div class="social-links">
        <a href="#" title="Twitter"><i class="fab fa-twitter"></i></a>

        <a href="https://www.instagram.com/codeex._.heoster" tittle="Instagram"><i class="fab fa-instagram"></i></a>
        <a href=" https://github.com/Heoster" title="GitHub"><i class="fab fa-github"></i></a>
      </div>
      <div class="footer-text">© 2025 Heoster's Wikinet AI. All rights reserved.</div>
      <div class="made-in-india">
        <span class="saffron">MADE</span>
        <span class="white">in</span>
        <span class="green">INDIA</span>
        <i class="fas fa-flag white"></i>
      </div>
    </footer>
  </div>

  <script>
    // Initialize chat with saved messages or welcome message
    document.addEventListener('DOMContentLoaded', function() {
      const savedChat = localStorage.getItem('chatHistory');
      if (savedChat) {
        document.getElementById('chatbox').innerHTML = savedChat;
        scrollToBottom();
      } else {
        showWelcomeMessage();
      }
      
      // Load quick suggestions
      showSuggestions();
      
      // Set up enter key listener
      document.getElementById('userInput').addEventListener('keypress', function(e) {
        if (e.key === 'Enter') {
          sendMessage();
        }
      });
    });

    function showWelcomeMessage() {
      const welcomeMessage = `
        <div class="info-message">Today is ${new Date().toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</div>
        <div class="bot-message">
          <strong>Welcome to Wikinet AI!</strong> 🌐<br><br>
          I'm your AI-powered knowledge assistant that can fetch information about:
          <ul style="margin-left: 20px; margin-top: 8px;">
            <li>Historical events and figures</li>
            <li>Scientific discoveries and theories</li>
            <li>Geographical locations and landmarks</li>
            <li>Technological advancements</li>
            <li>And virtually any topic covered on Wikipedia!</li>
          </ul>
          <div style="margin-top: 12px;">
            Try asking something like:<br>
            <em>"Tell me about quantum computing"</em><br>
            or<br>
            <em>"Who invented the telephone?"</em>
          </div>
          <div class="message-time">Just now</div>
        </div>
      `;
      document.getElementById('chatbox').innerHTML = welcomeMessage;
      saveChatHistory();
    }

    function showSuggestions() {
      const suggestions = [
        "Explain artificial intelligence",
        "History of the Roman Empire",
        "Biography of Marie Curie",
        "How does photosynthesis work?",
        "Latest space exploration missions",
        "Cultural significance of the Renaissance"
      ];
      
      const suggestionsHTML = suggestions.map(suggestion => 
        `<div class="suggestion-chip" onclick="insertSuggestion('${suggestion}')">${suggestion}</div>`
      ).join('');
      
      const suggestionsDiv = document.createElement('div');
      suggestionsDiv.className = 'suggestions';
      suggestionsDiv.innerHTML = suggestionsHTML;
      
      document.getElementById('chatbox').appendChild(suggestionsDiv);
      scrollToBottom();
    }

    function insertSuggestion(text) {
      document.getElementById('userInput').value = text;
      document.getElementById('userInput').focus();
    }

    async function sendMessage() {
      const userInput = document.getElementById("userInput");
      const message = userInput.value.trim();
      if (message === "") return;

      appendMessage("user", message);
      userInput.value = "";

      // Show typing indicator
      const typingDiv = document.createElement('div');
      typingDiv.className = 'typing-indicator';
      typingDiv.innerHTML = `
        <div class="typing-dot"></div>
        <div class="typing-dot"></div>
        <div class="typing-dot"></div>
      `;
      document.getElementById('chatbox').appendChild(typingDiv);
      scrollToBottom();

      try {
        const reply = await generateReply(message);
        
        // Remove typing indicator
        const typingIndicators = document.querySelectorAll('.typing-indicator');
        typingIndicators.forEach(indicator => indicator.remove());
        
        if (reply.isWikipedia) {
          appendWikipediaMessage(reply.title, reply.content, reply.url);
        } else {
          appendMessage("bot", reply);
        }
        
        // Show new suggestions after response
        showSuggestions();
      } catch (error) {
        console.error("Error generating reply:", error);
        appendMessage("bot", "Sorry, I encountered an error while processing your request. Please try again later.");
      }
    }

    function appendMessage(sender, text) {
      const chatbox = document.getElementById("chatbox");
      const msgDiv = document.createElement("div");
      msgDiv.className = sender === "user" ? "user-message" : "bot-message";
      
      const now = new Date();
      const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      
      msgDiv.innerHTML = `${text}<div class="message-time">${timeString}</div>`;
      chatbox.appendChild(msgDiv);
      
      saveChatHistory();
      scrollToBottom();
    }

    function appendWikipediaMessage(title, content, url) {
      const chatbox = document.getElementById("chatbox");
      const msgDiv = document.createElement("div");
      msgDiv.className = "wikipedia-message";
      
      const now = new Date();
      const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      
      // Shorten content if too long
      let shortenedContent = content;
      if (content.length > 500) {
        shortenedContent = content.substring(0, 500) + '...';
      }
      
      msgDiv.innerHTML = `
        <div class="wikipedia-title"><i class="fab fa-wikipedia-w"></i> Wikipedia: ${title}</div>
        ${shortenedContent}
        <a href="${url}" target="_blank" class="wikipedia-link">Read more on Wikipedia <i class="fas fa-external-link-alt"></i></a>
        <div class="message-time">${timeString}</div>
      `;
      chatbox.appendChild(msgDiv);
      
      saveChatHistory();
      scrollToBottom();
    }

    function scrollToBottom() {
      const chatbox = document.getElementById("chatbox");
      chatbox.scrollTop = chatbox.scrollHeight;
    }

    function saveChatHistory() {
      const chatbox = document.getElementById("chatbox");
      localStorage.setItem('chatHistory', chatbox.innerHTML);
    }

    async function fetchWikipediaData(searchTerm) {
      try {
        // First, search for the term to get the correct page title
        const searchUrl = `https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=${encodeURIComponent(searchTerm)}&format=json&origin=*`;
        
        const searchResponse = await fetch(searchUrl);
        const searchData = await searchResponse.json();
        
        if (searchData.query.search.length === 0) {
          return null;
        }
        
        const pageTitle = searchData.query.search[0].title;
        
        // Now fetch the page content
        const contentUrl = `https://en.wikipedia.org/w/api.php?action=query&prop=extracts&exintro=true&explaintext=true&titles=${encodeURIComponent(pageTitle)}&format=json&origin=*`;
        
        const contentResponse = await fetch(contentUrl);
        const contentData = await contentResponse.json();
        
        const pageId = Object.keys(contentData.query.pages)[0];
        const pageContent = contentData.query.pages[pageId].extract;
        const pageUrl = `https://en.wikipedia.org/wiki/${encodeURIComponent(pageTitle.replace(/ /g, '_'))}`;
        
        return {
          title: pageTitle,
          content: pageContent,
          url: pageUrl,
          isWikipedia: true
        };
      } catch (error) {
        console.error("Error fetching Wikipedia data:", error);
        return null;
      }
    }

    async function generateReply(message) {
      const lower = message.toLowerCase();
      const now = new Date();

      // Greetings
      if (lower.includes("hello") || lower.includes("hi") || lower.includes("hey")) {
        return `Hello there! 👋 I'm Wikinet AI, your knowledge assistant. Ask me about any topic and I'll fetch information for you!`;
      } 
      // Time
      else if (lower.includes("time")) {
        return `The current time is ${now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' })}`;
      } 
      // Date
      else if (lower.includes("date")) {
        return `Today is ${now.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}`;
      } 
      // Name
      else if (lower.includes("your name") || lower.includes("who are you")) {
        return "I'm Wikinet AI, your knowledge assistant! 🤖 I can fetch information to answer your questions about virtually any topic.";
      } 
      // Jokes
      else if (lower.includes("joke")) {
        const jokes = [
          "Why don't scientists trust atoms? Because they make up everything!",
          "Did you hear about the mathematician who's afraid of negative numbers? He'll stop at nothing to avoid them!",
          "Why don't skeletons fight each other? They don't have the guts!",
          "I told my wife she was drawing her eyebrows too high. She looked surprised.",
          "What do you call a fake noodle? An impasta!"
        ];
        return jokes[Math.floor(Math.random() * jokes.length)];
      } 
      // Creator
      else if (lower.includes("creator") || lower.includes("who made you") || lower.includes("who created you")) {
        return "I was developed by <strong>Heoster</strong> as a knowledge assistant, connecting to Wikipedia's API to provide comprehensive information.";
      } 
      // Goodbye
      else if (lower.includes("bye") || lower.includes("goodbye")) {
        return "Goodbye! 👋 Thank you for using Wikinet AI. Come back anytime you need information!";
      } 
      // Help
      else if (lower.includes("help") || lower.includes("what can you do")) {
        return `As Wikinet AI, I can fetch information about:
        • <strong>History</strong>: Events, periods, civilizations
        • <strong>Science</strong>: Concepts, discoveries, theories
        • <strong>People</strong>: Biographies of famous individuals
        • <strong>Geography</strong>: Countries, cities, landmarks
        • <strong>Technology</strong>: Innovations, computers, internet
        
        Try asking me something like:
        <em>"Tell me about the Great Wall of China"</em>
        or
        <em>"Explain quantum mechanics"</em>`;
      } 
      // Wikipedia queries
      else if (lower.includes("tell me about") || lower.includes("who is") || lower.includes("what is") || 
               lower.includes("explain") || lower.includes("information about") || 
               lower.includes("what do you know about")) {
        // Extract the search term
        let searchTerm = message;
        searchTerm = searchTerm.replace(/tell me about/gi, '');
        searchTerm = searchTerm.replace(/who is/gi, '');
        searchTerm = searchTerm.replace(/what is/gi, '');
        searchTerm = searchTerm.replace(/explain/gi, '');
        searchTerm = searchTerm.replace(/information about/gi, '');
        searchTerm = searchTerm.replace(/what do you know about/gi, '');
        searchTerm = searchTerm.trim();
        
        if (searchTerm.length === 0) {
          return "Please specify what you'd like to know about. For example: 'Tell me about the Eiffel Tower'";
        }
        
        const wikipediaData = await fetchWikipediaData(searchTerm);
        if (wikipediaData) {
          return wikipediaData;
        } else {
          return `I couldn't find information about "${searchTerm}" on Wikipedia. Try being more specific or check your spelling.`;
        }
      } 
      // Default - try to find in Wikipedia
      else {
        const wikipediaData = await fetchWikipediaData(message);
        if (wikipediaData) {
          return wikipediaData;
        }
        
        return "I'm not sure about that. Try asking me to 'tell you about' a specific topic, or ask a more specific question. For example: 'Tell me about the Renaissance' or 'Who invented the telephone?'";
      }
    }
  </script>
</body>
</html>
