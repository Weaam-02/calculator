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
  import { onMount } from "svelte";

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

      output?.classList.add("bg-red-500");

      setTimeout(() => {
        output?.classList.remove("bg-red-500");
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

  onMount(() => {
    let allBtn = document.getElementsByTagName("button");

    for (let i = 0; i < allBtn.length; i++) {
      allBtn[i].addEventListener("click", () => {
        new Audio("/meow-3.mp3").play();
      });
    }
  });
</script>

<svelte:window on:keydown|preventDefault={onKeyDown} />

<svelte:head>
  <title>My Cute Calc</title>
</svelte:head>

<!-- <div class="ear-l"></div>
<div class="ear-r"></div> -->

<!-- <div class="relative h-fit w-fit"> -->
<div
  class="ear a absolute left-[35.99rem] top-[3.95rem] h-16 w-16 -z-10 shadow-xl"
></div>
<div
  class="ear b absolute top-[3.95rem] right-[35.99rem] h-16 w-16 -z-10 shadow-xl"
></div>

<div
  class="bg-white max-w-[18.50rem] rounded-3xl grid grid-cols-4 gap-2 p-7 text-2xl font-semibold shadow-xl"
>
  <div class="bg-black w-4 h-4 rounded-full ml-16"></div>
  <!-- <div class="bg-black w-4 h-2 rounded-md col-span-2 ml-12 mt-2"></div> -->
  <!-- <div class="bg-black w-3 borde-b rounded-b-3xl col-span-2 ml-12 mt-2"></div> -->
  <div class="text-black font-extrabold col-span-2 mt-12 rotate-90">3</div>
  <div class="bg-black w-4 h-4 rounded-full -ml-8"></div>
  <div
    id="output"
    class="bg-[#ffb7bc] min-h-14 rounded-2xl flex items-center px-6 -mt-[3.4rem] mb-4 text-white col-span-4 shadow-lg break-all transition-all"
  >
    {equation}
  </div>

  <!-- "bg-slate-800 text-white hover:bg-slate-900 shadow-slate-800/80 -->

  <button
    on:click={clear}
    id="Delete"
    class="bg-slate-100 hover:bg-slate-200/50 active:bg-slate-200 transition-all"
  >
    AC
  </button>

  <button
    id="Backspace"
    on:click={() => backspace()}
    class="bg-slate-100 hover:bg-slate-200/50 active:bg-slate-200 transition-all"
  >
    <BackSpace />
  </button>

  <button
    id="%"
    on:click={() => addToEquation(" /100 ")}
    class="bg-slate-100 hover:bg-slate-200/50 font-extrabold active:bg-slate-200 transition-all"
  >
    %
  </button>

  <button
    id="+"
    on:click={() => addToEquation(" + ")}
    class="bg-red-200 text-white hover:bg-red-300/90 shadow-red-400/60"
  >
    <Plus />
  </button>

  <button id="7" on:click={() => addToEquation("7")}> 7 </button>
  <button id="8" on:click={() => addToEquation("8")}> 8 </button>
  <button id="9" on:click={() => addToEquation("9")}> 9 </button>
  <button
    id="-"
    on:click={() => addToEquation(" - ")}
    class="bg-red-300 text-white hover:bg-red-400/90 shadow-red-500/60"
  >
    <Minus />
  </button>

  <button id="4" on:click={() => addToEquation("4")}> 4 </button>
  <button id="5" on:click={() => addToEquation("5")}> 5 </button>
  <button id="6" on:click={() => addToEquation("6")}> 6 </button>
  <button
    id="/"
    on:click={() => addToEquation(" / ")}
    class="bg-red-400 text-white hover:bg-red-500/90 shadow-red-500/60"
  >
    <Divisionicon />
  </button>

  <button id="1" on:click={() => addToEquation("1")}> 1 </button>
  <button id="2" on:click={() => addToEquation("2")}> 2 </button>
  <button id="3" on:click={() => addToEquation("3")}> 3 </button>
  <button
    id="*"
    on:click={() => addToEquation(" * ")}
    class="bg-red-500 text-white hover:bg-red-600/90 shadow-red-500/60"
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
    class="bg-slate-100 hover:bg-slate-200 active:bg-slate-300 transition-all col-span-2"
  >
    <Equals />
  </button>
</div>
