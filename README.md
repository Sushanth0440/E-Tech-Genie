<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>E-Tech Genie Dashboard</title>
  <style>
    /* Reset and Base Styles */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      background: #f4f7f9;
      color: #333;
    }
    /* Sidebar Navigation (Fixed) */
    .sidebar {
      position: fixed;
      left: 0;
      top: 0;
      width: 220px;
      height: 100vh;
      background: linear-gradient(180deg, #004466, #006680);
      color: #fff;
      padding-top: 20px;
      overflow-y: auto;
    }
    .sidebar h2 {
      text-align: center;
      margin-bottom: 20px;
      font-size: 1.6em;
      border-bottom: 1px solid #fff;
      padding-bottom: 10px;
    }
    .sidebar ul {
      list-style: none;
      padding: 0;
    }
    .sidebar ul li {
      margin: 15px 0;
      text-align: center;
    }
    .sidebar ul li a {
      text-decoration: none;
      color: #fff;
      font-size: 1.1em;
      display: block;
      padding: 10px;
      transition: background 0.3s ease;
    }
    .sidebar ul li a:hover {
      background: rgba(255,255,255,0.3);
      border-radius: 4px;
    }
    /* Main Content Area */
    .main-content {
      margin-left: 240px;
      padding: 20px;
    }
    .page {
      display: none;
      animation: fadeIn 0.5s;
    }
    .page.active { display: block; }
    @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    /* Main Header for Each Page */
    .main-header {
      background: #0077cc;
      color: #fff;
      padding: 20px;
      margin-bottom: 20px;
      border-radius: 5px;
      text-align: center;
    }
    /* Card Styles (for Courses & Features Pages) */
    .card-container {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
    }
    .card {
      background: #fff;
      padding: 15px;
      border-radius: 5px;
      box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
      width: 300px;
      transition: transform 0.3s ease;
    }
    .card:hover { transform: scale(1.02); }
    .card h3 { margin-bottom: 10px; color: #0077cc; }
    .card p { font-size: 0.95em; margin-bottom: 10px; }
    .card a {
      display: inline-block;
      margin-top: 10px;
      padding: 8px 12px;
      background: #0077cc;
      color: #fff;
      text-decoration: none;
      border-radius: 4px;
    }
    /* Resources Page - Only Nihir Shah Content */
    .nihir-resource {
      background: #fff;
      padding: 20px;
      border-radius: 5px;
      margin: auto;
      max-width: 600px;
      box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
    }
    .nihir-resource h3 { text-align: center; margin-bottom: 15px; }
    .nihir-resource ul { list-style: disc; margin-left: 20px; }
    .nihir-resource a { 
      color: #0077cc; 
      text-decoration: none; 
    }
    .nihir-resource a:hover { text-decoration: underline; }
    /* Quiz Page */
    .quiz form { max-width: 600px; margin: auto; }
    .quiz .quiz-question { margin-bottom: 20px; }
    .quiz .quiz-question p { font-weight: bold; margin-bottom: 8px; }
    .quiz label { display: block; padding: 5px; }
    .quiz button {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      background: #0077cc;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    /* Chat Page - Dictionary Search Interface */
    .chat-box {
      max-width: 600px;
      margin: 40px auto;
      display: flex;
      flex-direction: column;
    }
    .chat-window {
      background: #f1f1f1;
      border: 1px solid #ccc;
      border-radius: 5px;
      height: 300px;
      overflow-y: auto;
      padding: 10px;
      margin-bottom: 10px;
    }
    .chat-message {
      margin: 5px 0;
      padding: 8px;
      border-radius: 5px;
    }
    .chat-message.user { background: #d1e7dd; text-align: right; }
    .chat-message.bot { background: #f8d7da; text-align: left; }
    /* Contact Page */
    .contact-form {
      max-width: 600px;
      margin: auto;
      text-align: left;
    }
    .contact-form label {
      display: block;
      margin: 10px 0 5px;
      font-weight: bold;
    }
    .contact-form input, .contact-form textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .contact-form button {
      margin-top: 10px;
      padding: 10px 20px;
      background: #0077cc;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    /* Footer */
    footer {
      background: #004466;
      color: #fff;
      padding: 15px;
      text-align: center;
      margin-top: 20px;
    }
    /* Welcome Bot Modal */
    .modal {
      display: none;
      position: fixed;
      z-index: 100;
      padding-top: 100px;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
    }
    .modal-content {
      background: #fff;
      margin: auto;
      padding: 20px;
      border-radius: 10px;
      width: 80%;
      max-width: 400px;
      text-align: center;
    }
    .modal-content h2 { color: #0077cc; }
    .modal-content p { font-size: 1.1em; margin-bottom: 15px; }
    .modal-content button {
      margin-top: 20px;
      padding: 10px 20px;
      background: #0077cc;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .modal-content .bot-img {
      border-radius: 50%;
      margin-bottom: 10px;
    }
    .close {
      position: absolute;
      top: 10px;
      right: 15px;
      color: #aaa;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
    }
    .close:hover, .close:focus {
      color: #000;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <!-- Sidebar Navigation -->
  <div class="sidebar">
    <h2>E-Tech Genie</h2>
    <ul>
      <li><a href="#" onclick="showPage('home')">Home</a></li>
      <li><a href="#" onclick="showPage('courses')">Courses</a></li>
      <li><a href="#" onclick="showPage('features')">Features</a></li>
      <li><a href="#" onclick="showPage('resources')">Resources</a></li>
      <li><a href="#" onclick="showPage('quiz')">Quiz</a></li>
      <li><a href="#" onclick="showPage('chat')">Dictionary</a></li>
      <li><a href="#" onclick="showPage('contact')">Contact</a></li>
    </ul>
  </div>

  <!-- Main Content Area -->
  <div class="main-content">
    <!-- Home Page -->
    <div id="home" class="page active">
      <div class="main-header">
        <h1>Welcome to E-Tech Genie Dashboard</h1>
      </div>
      <p>
        E-Tech Genie is a cutting-edge smart learning platform trusted by hundreds of schools nationwide.
        Our interactive courses, personalized feedback, and integrated educational tools empower students and educators alike.
        Discover the future of education and join the revolution today!
      </p>
      <br />
      <button onclick="showPage('courses')">Explore Our Courses</button>
    </div>
    
    <!-- Courses Page -->
    <div id="courses" class="page">
      <div class="main-header">
        <h1>Our Courses</h1>
      </div>
      <div class="card-container">
        <div class="card">
          <h3>Basic English Grammar</h3>
          <p>Learn essentials of grammar, sentence structure, and vocabulary.</p>
          <a href="https://www.youtube.com/embed/H9rcifEcS2k" target="_blank">Watch Intro Video</a>
        </div>
        <div class="card">
          <h3>Conversational English</h3>
          <p>Improve your speaking skills with real-life interactive dialogues.</p>
          <a href="https://www.youtube.com/embed/2Nf43kbbF9g" target="_blank">Watch Overview</a>
        </div>
        <div class="card">
          <h3>Advanced Writing</h3>
          <p>Enhance your creativity and clarity with advanced writing techniques.</p>
          <a href="https://www.youtube.com/embed/m9drsetQbRU" target="_blank">Watch Overview</a>
        </div>
      </div>
    </div>
    
    <!-- Features Page -->
    <div id="features" class="page">
      <div class="main-header">
        <h1>Key Features</h1>
      </div>
      <div class="card-container">
        <div class="card">
          <h3>Adaptive Learning</h3>
          <p>Lessons tailored to your progress for a personalized pace.</p>
        </div>
        <div class="card">
          <h3>Interactive Quizzes</h3>
          <p>Receive immediate feedback and track your improvement in real time.</p>
        </div>
        <div class="card">
          <h3>Progress Dashboard</h3>
          <p>Monitor your growth with detailed analytics and custom reports.</p>
        </div>
      </div>
    </div>
    
    <!-- Resources Page (Only Nihir Shah Content) -->
    <div id="resources" class="page">
      <div class="main-header">
        <h1>Learning Resources</h1>
      </div>
      <div class="nihir-resource">
        <h3>Nihir Shah - English Grammar &amp; Composition</h3>
        <p>
          Nihir Shah's YouTube channel focuses on English grammar and composition.
          His tutorials cover topics such as:
        </p>
        <ul>
          <li>Report Writing [1]</li>
          <li>Modal Verbs [3]</li>
          <li>Subject-Verb Agreement [4]</li>
          <li>Tenses [5]</li>
          <li>Verbs [6]</li>
          <li>Wren &amp; Martin English Grammar Book [2]</li>
        </ul>
        <h4>Sources</h4>
        <ul>
          <li><a href="https://www.youtube.com/c/nihirshah" target="_blank">Nihir Shah's YouTube Channel</a></li>
          <li><a href="https://www.youtube.com/watch?v=cqTa2aV8LTY" target="_blank">English Grammar and Composition | Wren and Martin ...</a></li>
          <li><a href="https://www.youtube.com/watch?v=q2rKXa3FOZ4" target="_blank">All about Modal Verbs | Defective Verbs | Auxiliary Verbs ...</a></li>
          <li><a href="https://www.youtube.com/watch?v=5dNAffCFNNI" target="_blank">Subject-Verb Agreement | Six Important Rules | Part 2</a></li>
          <li><a href="https://www.youtube.com/watch?v=g0HUqeghtJI" target="_blank">Learn Tenses Easily: Master the Fundamentals of English ...</a></li>
          <li><a href="https://m.youtube.com/watch?v=z96-ZkIpQZQ&t=42s" target="_blank">Learn all about Verbs | Main Verbs | Auxiliary Verbs !</a></li>
        </ul>
      </div>
    </div>
    
    <!-- Quiz Page -->
    <div id="quiz" class="page">
      <div class="main-header">
        <h1>Quick Quiz</h1>
      </div>
      <form id="quizForm">
        <div class="quiz-question">
          <p>1. What is the correct plural of "child"?</p>
          <label><input type="radio" name="q1" value="wrong" /> Childs</label>
          <label><input type="radio" name="q1" value="correct" /> Children</label>
          <label><input type="radio" name="q1" value="wrong" /> Childer</label>
          <label><input type="radio" name="q1" value="wrong" /> Childrens</label>
        </div>
        <div class="quiz-question">
          <p>2. Which sentence is grammatically correct?</p>
          <label><input type="radio" name="q2" value="wrong" /> He don't like apples.</label>
          <label><input type="radio" name="q2" value="correct" /> He doesn't like apples.</label>
          <label><input type="radio" name="q2" value="wrong" /> He not likes apples.</label>
          <label><input type="radio" name="q2" value="wrong" /> He no like apples.</label>
        </div>
        <div class="quiz-question">
          <p>3. Choose the synonym for "commence".</p>
          <label><input type="radio" name="q3" value="correct" /> Begin</label>
          <label><input type="radio" name="q3" value="wrong" /> End</label>
          <label><input type="radio" name="q3" value="wrong" /> Pause</label>
          <label><input type="radio" name="q3" value="wrong" /> Stop</label>
        </div>
        <button type="button" onclick="checkQuiz()">Submit Answers</button>
      </form>
    </div>
    
    <!-- Chat Page (Dictionary Search using CoPilot) -->
    <div id="chat" class="page">
      <div class="main-header">
        <h1>CoPilot Dictionary Search</h1>
      </div>
      <div class="chat-box">
        <div id="chatWindow" class="chat-window"></div>
        <input type="text" id="userInput" placeholder="Type a word or phrase (e.g., 'define grammar')..." />
        <button onclick="sendMessage()">Search</button>
      </div>
    </div>
    
    <!-- Contact Page -->
    <div id="contact" class="page">
      <div class="main-header">
        <h1>Contact Us</h1>
      </div>
      <div class="contact-form">
        <form id="contactForm">
          <label for="name">Name:</label>
          <input type="text" id="name" name="name" required />
          <label for="email">Email:</label>
          <input type="email" id="email" name="email" required />
          <label for="message">Message:</label>
          <textarea id="message" name="message" rows="5" required></textarea>
          <button type="button" onclick="submitContact()">Send Message</button>
        </form>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 E-Tech Genie | Smart Learning for All</p>
  </footer>
  
  <script>
    // Function to display a specific page and hide the others
    function showPage(pageId) {
      var pages = document.getElementsByClassName('page');
      for (var i = 0; i < pages.length; i++) {
        pages[i].classList.remove('active');
      }
      document.getElementById(pageId).classList.add('active');
    }
    
    // Welcome Bot Modal Functionality
    document.addEventListener('DOMContentLoaded', function () {
      var modal = document.getElementById('welcome-bot');
      var closeBtn = document.getElementsByClassName('close')[0];
      var startButton = document.getElementById('startButton');
      setTimeout(function() { modal.style.display = 'block'; }, 1000);
      closeBtn.onclick = function() { modal.style.display = 'none'; };
      startButton.onclick = function() { modal.style.display = 'none'; };
      window.onclick = function(event) {
        if (event.target === modal) { modal.style.display = 'none'; }
      };
    });
    
    // Quiz Evaluation Functionality
    function checkQuiz() {
      var score = 0;
      var totalQuestions = 3;
      var form = document.getElementById('quizForm');
      if (form.elements['q1'].value === "correct") score++;
      if (form.elements['q2'].value === "correct") score++;
      if (form.elements['q3'].value === "correct") score++;
      alert('Your score is ' + score + ' out of ' + totalQuestions);
    }
    
    // Dummy Contact Form Submission
    function submitContact() {
      var form = document.getElementById('contactForm');
      if (form.elements['name'].value && form.elements['email'].value && form.elements['message'].value) {
        alert('Thank you, ' + form.elements['name'].value + '! Your message has been submitted.');
        form.reset();
      } else {
        alert('Please fill in all the fields.');
      }
    }
    
    // CoPilot Dictionary Search Functionality
    async function getDictionaryAnswer(query) {
      // Remove extra spaces and convert to lower case.
      let trimmedQuery = query.trim();
      let lowerQuery = trimmedQuery.toLowerCase();
      
      // If the query starts with "define", extract the next word.
      let word = "";
      if (lowerQuery.startsWith("define ")) {
        word = lowerQuery.substring(7).split(" ")[0];
      } else {
        // For a single-word query, use it; otherwise, pick the last word.
        let words = lowerQuery.split(" ");
        if (words.length === 1) {
          word = words[0];
        } else {
          word = words[words.length - 1].replace(/[.,?!]/g, "");
        }
      }
      
      // Simulated CoPilot Dictionary definitions
      const dictionary = {
        "apple": "A round fruit with red, yellow, or green skin and a sweet taste.",
        "grammar": "The structural rules governing the composition of clauses, phrases, and words in a language.",
        "technology": "The application of scientific knowledge for practical purposes, especially in industry.",
        "learning": "The process of acquiring knowledge or skills through study, experience, or teaching.",
        "copilot": "Your AI companion that assists you with information retrieval and guidance."
      };
      
      if (dictionary[word]) {
        return "Definition: " + word + " - " + dictionary[word];
      } else {
        return "Definition: No definition found for \"" + word + "\".";
      }
    }
    
    async function sendMessage() {
      var userInput = document.getElementById("userInput");
      var message = userInput.value.trim();
      if (message !== "") {
        appendMessage("user", message);
        userInput.value = "";
        // Instead of a general web search, we now perform a dictionary lookup using our simulated CoPilot Dictionary.
        var response = await getDictionaryAnswer(message);
        // Do not reveal any search specifics.
        appendMessage("bot", response);
      }
    }
    
    function appendMessage(sender, message) {
      var chatWindow = document.getElementById("chatWindow");
      var messageDiv = document.createElement("div");
      messageDiv.className = "chat-message " + sender;
      messageDiv.textContent = message;
      chatWindow.appendChild(messageDiv);
      chatWindow.scrollTop = chatWindow.scrollHeight;
    }
  </script>
  
  <!-- Welcome Bot Modal -->
  <div id="welcome-bot" class="modal">
    <div class="modal-content">
      <span class="close">&times;</span>
      <img src="https://via.placeholder.com/100?text=GenieBot" alt="GenieBot" class="bot-img" />
      <h2>Welcome to E-Tech Genie!</h2>
      <p>Hello! I’m GenieBot, your guide to a smarter learning journey.</p>
      <button id="startButton">Let's Begin</button>
    </div>
  </div>
</body>
</html>
