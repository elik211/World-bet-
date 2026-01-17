<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mines Demo Skeleton</title>
  <style>
    body { background:#111; color:#fff; font-family:Arial; text-align:center; }
    .grid { display:grid; grid-template-columns:repeat(5,60px); gap:10px; justify-content:center; margin-top:20px;}
    .cell { width:60px; height:60px; background:#222; cursor:pointer; font-size:24px; display:flex; align-items:center; justify-content:center; }
    .revealed { background:#444; }
    .mine { background:red; }
  </style>
</head>
<body>
<h1>Mines Demo Skeleton</h1>
<div class="grid" id="grid"></div>
<p id="status"></p>

<script>
const grid = document.getElementById('grid');
const size = 25; // 5x5
let cells = [];

function createGrid() {
  for(let i=0; i<size; i++){
    const cell = document.createElement('div');
    cell.classList.add('cell');
    cell.dataset.index = i;
    cell.addEventListener('click', clickCell);
    grid.appendChild(cell);
    cells.push(cell);
  }
}

function clickCell(e){
  const cell = e.target;
  if(cell.classList.contains('revealed')) return;

  cell.classList.add('revealed');

  // Demo random mine, heç real pul yoxdur
  const isMine = Math.random() < 0.2; // 20% mine
  if(isMine){
    cell.classList.add('mine');
    cell.innerText = "💣";
    document.getElementById('status').innerText = "Boom! Mine clicked.";
    revealAll();
  } else {
    cell.innerText = "✅";
  }
}

function revealAll(){
  cells.forEach(c => {
    if(!c.classList.contains('revealed')){
      c.classList.add('revealed');
      if(Math.random() < 0.2) c.classList.add('mine');
    }
  });
}

createGrid();
</script>
</body>
</html>
