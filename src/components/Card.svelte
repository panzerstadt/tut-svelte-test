<script>
  import { fade, fly } from "svelte/transition";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  let mouse = { x: 0, y: 0 };
  let aMouseX = tweened(0, { duration: 400, easing: cubicOut });
  let aMouseY = tweened(0, { duration: 400, easing: cubicOut });

  let offsetPoster = 2;
  $: transformPoster = transformCard($aMouseX, $aMouseY);

  function handleMouseMove(e) {
    mouse = { x: e.clientX, y: e.clientY };
    aMouseX.set(e.clientX);
    aMouseY.set(e.clientY);
  }
  function resetMouseMove(e) {
    mouse = { x: 0, y: 0 };
    aMouseX.set(0);
    aMouseY.set(0);
  }

  function transformCard(mouseX, mouseY) {
    // https://codepen.io/VinderOrnitier/pen/JYMJNb
    let x = mouseX;
    let y = mouseY;
    let w = window.innerWidth;
    let h = window.innerHeight;

    let offsetX = 0.5 - x / w; //cursor position X
    let offsetY = 0.5 - y / h; //cursor position Y
    let dy = y - h / 2; //@h/2 = center of poster
    let dx = x - w / 2; //@w/2 = center of poster
    let theta = Math.atan2(dy, dx); //angle between cursor and center of poster in RAD
    let angle = (theta * 180) / Math.PI - 90; //convert rad in degrees

    let transform =
      "translateY(" +
      -offsetX * offsetPoster +
      "px) rotateX(" +
      -offsetY * offsetPoster +
      "deg) rotateY(" +
      offsetX * (offsetPoster * 2) +
      "deg)"; //poster transform

    return transform;
  }
</script>

<style>
  .container {
    position: relative;

    width: calc(100% - 80px);
    min-height: 200px;
    box-shadow: 1px 2px 12px rgba(0, 0, 0, 0.075);
    border-radius: 15px;
    padding: 20px;
    border: 1px solid rgba(0, 0, 0, 0.055);
    margin: 5px 20px;

    transform-style: preserve-3d;
  }

  .ref {
    position: absolute;
    bottom: 0;
    right: 20px;

    font-size: 10px;
    color: lightgray;
  }
</style>

<div
  transition:fly={{ y: 200 }}
  style={`transform: perspective(1500px) ${transformPoster}`}
  on:mousemove={handleMouseMove}
  on:mouseout={resetMouseMove}
  class="container">

  <slot />
  <p class="ref">x: {mouse.x} y: {mouse.y}</p>
</div>
