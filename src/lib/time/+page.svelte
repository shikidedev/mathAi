<script lang="ts">
    let question: string = '';
    let answer: string = '';
    let userAnswer: string = '';
    let feedback: string = '';
  
    // Function to generate random hours and minutes
    function getRandomTime(): { hour: number, minute: number } {
      const hour: number = Math.floor(Math.random() * 12) + 1; // Random hour between 1 and 12
      const minute: number = Math.floor(Math.random() * 60);   // Random minute between 0 and 59
      return { hour, minute };
    }
  
    // Function to format time
    function formatTime(hour: number, minute: number): string {
      return `${hour}:${minute.toString().padStart(2, '0')}`;
    }
  
    // Function to generate a random question about time
    function generateQuestion(): void {
      const { hour, minute } = getRandomTime();
      question = `What time is it? The clock shows ${formatTime(hour, minute)}.`;
      answer = `${hour}:${minute.toString().padStart(2, '0')}`;
      feedback = '';
      userAnswer = '';
    }
  
    // Check user's answer
    function checkAnswer(): void {
      feedback = userAnswer === answer ? 'Correct!' : `Oops! The correct answer is ${answer}.`;
    }
  
    // Generate the first question on load
    generateQuestion();
  </script>
  
  <main>
    <h1>Time Question Generator for Kids</h1>
    <p>{question}</p>
  
    <input type="text" bind:value={userAnswer} placeholder="Enter your answer (HH:MM)" />
    <button on:click={checkAnswer}>Check Answer</button>
  
    <p>{feedback}</p>
    <button on:click={generateQuestion}>New Question</button>
  </main>
  
  <style>
    main {
      text-align: center;
      padding: 2rem;
      font-family: Arial, sans-serif;
    }
  
    input {
      padding: 0.5rem;
      margin: 0.5rem;
      font-size: 1.2rem;
    }
  
    button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      cursor: pointer;
    }
  </style>
  