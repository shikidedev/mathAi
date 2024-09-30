<script lang="ts">
  import { onMount } from 'svelte';

  let operation: string = '';
  let num1: number = 0;
  let num2: number = 0;
  let userAnswer: number = 0;
  let feedback: string = '';
  let correctAnswer: number = 0;

  // Function to generate a random math problem
  function generateMathProblem() {
    const operations = ['+', '-', '*', '/'];
    operation = operations[Math.floor(Math.random() * operations.length)];
    num1 = Math.floor(Math.random() * 10) + 1; // Random number between 1 and 10
    num2 = Math.floor(Math.random() * 10) + 1; // Random number between 1 and 10

    // Handle division to avoid dividing by zero
    if (operation === '/') {
      num1 *= num2; // Ensure num1 is a multiple of num2
    }

    // Calculate the correct answer based on the operation
    switch (operation) {
      case '+':
        correctAnswer = num1 + num2;
        break;
      case '-':
        correctAnswer = num1 - num2;
        break;
      case '*':
        correctAnswer = num1 * num2;
        break;
      case '/':
        correctAnswer = num1 / num2;
        break;
    }
  }

  // Function to check the user's answer
  function checkAnswer() {
    if (userAnswer === correctAnswer) {
      feedback = 'Correct!';
    } else {
      feedback = `Incorrect! The correct answer was ${correctAnswer}.`;
    }
  }

  // Generate the first problem on mount
  onMount(() => {
    generateMathProblem();
  });
</script>

<main>
  <h1>Solve the Math Problem!</h1>
  <p>
    What is {num1} {operation} {num2}?
  </p>
  <input
    type="number"
    bind:value={userAnswer}
    placeholder="Your answer"
  />
  <button on:click={checkAnswer}>Submit Answer</button>
  <p>{feedback}</p>
  <button on:click={() => { generateMathProblem(); userAnswer = 0; feedback = ''; }}>
    Next Problem
  </button>
</main>

<style>
  main {
    text-align: center;
    padding: 2rem;
    font-family: Arial, sans-serif;
  }
  input {
    margin: 1rem 0;
    padding: 0.5rem;
  }
  button {
    margin: 0.5rem;
    padding: 0.5rem 1rem;
  }
</style>
