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

  // TODO: fix remove space
  function backSpace() {
    equation = equation.substring(0, equation.length - 1);
  }

  function clear() {
    equation = "";
  }

  function solve() {
    equation = eval(equation);
  }

  let equation: string = "";
</script>

<svelte:head>
  <title>My Cute Calc</title>
</svelte:head>

<div
  class="bg-white rounded-2xl grid grid-cols-4 gap-2 p-7 text-2xl font-semibold shadow-2xl"
>
  <div
    class="bg-blue-400 h-14 rounded-full flex items-center px-6 my-4 text-white col-span-4 shadow-lg shadow-blue-400/50"
  >
    {equation}
  </div>

  <!-- "bg-slate-800 text-white hover:bg-slate-900 shadow-slate-800/80 -->

  <button on:click={clear} class="bg-slate-100 hover:bg-slate-200/50">
    AC
  </button>

  <button on:click={backSpace} class="bg-slate-100 hover:bg-slate-200/50">
    <BackSpace />
  </button>

  <button
    on:click={() => addToEquation(" /100 ")}
    class="bg-slate-100 hover:bg-slate-200/50 font-extrabold"
  >
    %
  </button>

  <button
    on:click={() => addToEquation(" + ")}
    class="bg-green-400 text-white hover:bg-green-500/80 shadow-green-400/80"
  >
    <Plus />
  </button>

  <button on:click={() => addToEquation("7")}> 7 </button>
  <button on:click={() => addToEquation("8")}> 8 </button>
  <button on:click={() => addToEquation("9")}> 9 </button>
  <button
    on:click={() => addToEquation(" - ")}
    class="bg-red-500 text-white hover:bg-red-600/90 shadow-red-500/60"
  >
    <Minus />
  </button>

  <button on:click={() => addToEquation("4")}> 4 </button>
  <button on:click={() => addToEquation("5")}> 5 </button>
  <button on:click={() => addToEquation("6")}> 6 </button>
  <button
    on:click={() => addToEquation(" / ")}
    class="bg-blue-500 text-white hover:bg-blue-600/90 shadow-blue-500/80"
  >
    <Divisionicon />
  </button>

  <button on:click={() => addToEquation("1")}> 1 </button>
  <button on:click={() => addToEquation("2")}> 2 </button>
  <button on:click={() => addToEquation("3")}> 3 </button>
  <button
    on:click={() => addToEquation(" * ")}
    class="bg-yellow-400 text-white hover:bg-yellow-400/90 shadow-yellow-400/80"
  >
    <Multi />
  </button>

  <button on:click={() => addToEquation(" . ")} class="font-extrabold">
    .
  </button>
  <button on:click={() => addToEquation("0")}> 0 </button>
  <button
    on:click={() => solve()}
    class="bg-slate-100 hover:bg-slate-200/50 col-span-2"
  >
    <Equals />
  </button>
</div>
