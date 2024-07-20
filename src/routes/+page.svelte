<!-- <h1>Welcome to My Cute Calc</h1>
<!-- <script lang="ts">
  let x = 1;

  function multipy() {
    x *= 2;
  }

  function divide() {
    x /= 2;
  }
</script>

<div class="bg-black mt-10 mr-10 ml-10 border-red-400 border-4 rounded">
  <h1 class="text-5xl text-center text-red-400 mt-10 mb-10">Counter</h1>
  <h1 class="text-5xl text-center text-red-300 mb-10">|| {x} ||</h1>
  <button
    on:click={multipy}
    class="text-4xl text-center text-red-400 border-red-400 border-4 mr-48 ml-96 mb-10 p-2"
  >
    Multipy
  </button>
  <button
    on:click={divide}
    class="text-4xl text-center text-red-400 border-red-400 border-4 ml-96 p-2"
  >
    Divide
  </button>
</div> -->
<!-- .................................................. -->

<script lang="ts">
  import BackSpace from "$lib/icons/backSpace.svelte";
  import Divisionicon from "$lib/icons/division.svelte";
  import Plus from "$lib/icons/plus.svelte";
  import Multi from "$lib/icons/multi.svelte";
  import Minus from "$lib/icons/minus.svelte";
  import Equals from "$lib/icons/equals.svelte";

  function addToEquation(value: string) {
    equation += value;
  }

  function backspace() {
    switch (equation.substring(equation.length - 3, equation.length)) {
      case " + ":
      case " * ":
      case " - ":
      case " / ":
        equation = equation.substring(0, equation.length - 3);
        break;
      default:
        equation = equation.substring(0, equation.length - 1);
    }
  }

  function clear() {
    equation = "";
  }

  function solve() {
    try {
      let answer = eval(equation);
      if (answer == undefined) throw SyntaxError;
      equation = answer;
    } catch (error) {
      let output = document.getElementById("output");

      output?.classList.add("bg-red-600/90");

      setTimeout(() => {
        output?.classList.remove("bg-red-600/90");
      }, 500);
    }
  }

  let equation: string = "";

  function onKeyDown(e: KeyboardEvent) {
    let button = document.getElementById(e.key);

    button?.click();

    button?.focus();

    setTimeout(() => {
      //@ts-ignore
      document.activeElement?.blur();
    }, 100);
  }
</script>

<svelte:window on:keydown|preventDefault={onKeyDown} />

<svelte:head>
  <title>My Cute Calc</title>
</svelte:head>

<div
  class="bg-white max-w-[18.50rem] rounded-2xl grid grid-cols-4 gap-2 p-7 text-2xl font-semibold shadow-2xl"
>
  <div
    id="output"
    class="bg-blue-400 min-h-14 rounded-2xl flex items-center px-6 my-2 mb-4 text-white col-span-4 shadow-lg shadow-blue-400/50 break-all transition-all"
  >
    {equation}
  </div>

  <!-- "bg-slate-800 text-white hover:bg-slate-900 shadow-slate-800/80 -->

  <button
    on:click={clear}
    id="Delete"
    class="bg-slate-100 hover:bg-slate-200/50 active:bg-slate-300 transition-all"
  >
    AC
  </button>

  <button
    id="Backspace"
    on:click={() => backspace()}
    class="bg-slate-100 hover:bg-slate-200/50 active:bg-slate-300 transition-all"
  >
    <BackSpace />
  </button>

  <button
    id="%"
    on:click={() => addToEquation(" /100 ")}
    class="bg-slate-100 hover:bg-slate-200/50 font-extrabold active:bg-slate-300 transition-all"
  >
    %
  </button>

  <button
    id="+"
    on:click={() => addToEquation(" + ")}
    class="bg-green-400 text-white hover:bg-green-500/80 shadow-green-400/80"
  >
    <Plus />
  </button>

  <button id="7" on:click={() => addToEquation("7")}> 7 </button>
  <button id="8" on:click={() => addToEquation("8")}> 8 </button>
  <button id="9" on:click={() => addToEquation("9")}> 9 </button>
  <button
    id="-"
    on:click={() => addToEquation(" - ")}
    class="bg-red-500 text-white hover:bg-red-600/90 shadow-red-500/60"
  >
    <Minus />
  </button>

  <button id="4" on:click={() => addToEquation("4")}> 4 </button>
  <button id="5" on:click={() => addToEquation("5")}> 5 </button>
  <button id="6" on:click={() => addToEquation("6")}> 6 </button>
  <button
    id="/"
    on:click={() => addToEquation(" / ")}
    class="bg-blue-500 text-white hover:bg-blue-600/90 shadow-blue-500/80"
  >
    <Divisionicon />
  </button>

  <button id="1" on:click={() => addToEquation("1")}> 1 </button>
  <button id="2" on:click={() => addToEquation("2")}> 2 </button>
  <button id="3" on:click={() => addToEquation("3")}> 3 </button>
  <button
    id="*"
    on:click={() => addToEquation(" * ")}
    class="bg-yellow-400 text-white hover:bg-yellow-400/90 shadow-yellow-400/80"
  >
    <Multi />
  </button>

  <button id="." on:click={() => addToEquation(" . ")} class="font-extrabold">
    .
  </button>
  <button id="0" on:click={() => addToEquation("0")}> 0 </button>
  <button
    id="="
    on:click={() => solve()}
    class="bg-slate-100 hover:bg-slate-200/50 active:bg-slate-300 transition-all col-span-2"
  >
    <Equals />
  </button>
</div>
