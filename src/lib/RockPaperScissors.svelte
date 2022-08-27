<script lang="ts">
  import rock from "../assets/rock-svgrepo-com.svg";
  import paper from "../assets/toilet-paper-svgrepo-com.svg";
  import scissors from "../assets/scissors-svgrepo-com.svg";

  type Choice = "rock" | "paper" | "scissors" | null;
  type Result = "You Won" | "You Lost" | "Tie" | null;
  const arr = ["rock", "paper", "scissors"];

  var playerChoice: Choice = null;
  var computerChoice;
  var result: Result = null;
  var disabled: string = "";

  function Rock() {
    playerChoice = "rock";
    disabled = "disabled";
    checkWinner();
  }
  function Paper() {
    playerChoice = "paper";
    disabled = "disabled";
    checkWinner();
  }
  function Scissors() {
    playerChoice = "scissors";
    disabled = "disabled";
    checkWinner();
  }

  function checkWinner(): void {
    computerChoice = arr[Math.floor(Math.random() * arr.length)];

    if (
            computerChoice === "rock" && playerChoice === "scissors" ||
            computerChoice === "paper" && playerChoice === "rock" ||
            computerChoice === "scissors" && playerChoice === "paper"
    ) {
      result = "You Lost";
    } else if (
            computerChoice === playerChoice
    ) {
      result = "Tie"
    } else {
      result = "You Won";
    }
  }

  function playAgain() {
    playerChoice = null;
    computerChoice = null;
    result = null;
    disabled = "";
  }
</script>

<section>
  <article class="buttons">
    <div class="rock">
      <button on:click={Rock} disabled='{disabled}'>
        <img src={rock} alt="rock" />
      </button>
    </div>
    <div class="paper">
      <button on:click={Paper} disabled='{disabled}'>
        <img src={paper} width="120px" height="120px" alt="rock" />
      </button>
    </div>
    <div class="scissors">
      <button on:click={Scissors} disabled='{disabled}'>
        <img src={scissors} width="120px" height="120px" alt="rock" />
      </button>
    </div>
  </article>
  <article class="info">
    <div class="computer-choice">
      <h3>
        Computer choose: {computerChoice || "..."}
      </h3>
    </div>
    <div class="result">
      <h2 class:active={playerChoice !== null}>
        {result}
      </h2>
      <button
              class:active={result !== null}
              class="play-again"
              on:click={playAgain}
      >
        Play again
      </button>
    </div>
  </article>
</section>

<style>
  .result h2,
  .result button
  {
    display: none;
  }

  .result {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .info button {
    background: #213547;
    border-radius: 10px;
    border: 1px solid transparent;
    transition: 300ms ease-in-out;
    width: fit-content;
  }

  .info button:hover {
    border-color: #535bf2;
  }

  h3 {
    text-transform: capitalize;
  }

  .result .active {
    display: block;
  }

  button {
    background: none;
    outline: none;
    border: none;
    padding: 1em;
    font-size: 1em;
    transition: 300ms ease-in-out;
    cursor: pointer;
  }
  .buttons button:hover {
    transform: scale(1.1);
  }
  button:focus {
    border: none;
  }

  .buttons {
    display: inline-flex;
    gap: 5em;
  }
</style>