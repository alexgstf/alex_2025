---
layout: blank
title: Minesweeper
permalink: /minesweeper
---
<a href="/alex_2025/">Home</a>

<div id="minesweeper"></div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    const rows = 10;
    const cols = 10;
    const mineCount = 10;
    const cellSize = 30;
    const grid = [];
    let revealedCount = 0;

    function initGame() {
        for (let r = 0; r < rows; r++) {
            grid[r] = [];
            for (let c = 0; c < cols; c++) {
                grid[r][c] = { isMine: false, isRevealed: false, adjacentMines: 0 };
            }
        }

        // Place mines
        let minesPlaced = 0;
        while (minesPlaced < mineCount) {
            const r = Math.floor(Math.random() * rows);
            const c = Math.floor(Math.random() * cols);
            if (!grid[r][c].isMine) {
                grid[r][c].isMine = true;
                minesPlaced++;
                updateAdjacentMines(r, c);
            }
        }

        render();
    }

    function updateAdjacentMines(r, c) {
        for (let dr = -1; dr <= 1; dr++) {
            for (let dc = -1; dc <= 1; dc++) {
                const nr = r + dr;
                const nc = c + dc;
                if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && !(dr === 0 && dc === 0)) {
                    grid[nr][nc].adjacentMines++;
                }
            }
        }
    }

    function render() {
        const container = document.getElementById('minesweeper');
        container.innerHTML = '';
        const table = document.createElement('table');
        table.style.borderCollapse = 'collapse';
        container.appendChild(table);

        for (let r = 0; r < rows; r++) {
            const row = document.createElement('tr');
            table.appendChild(row);
            for (let c = 0; c < cols; c++) {
                const cell = document.createElement('td');
                cell.style.width = `${cellSize}px`;
                cell.style.height = `${cellSize}px`;
                cell.style.border = '1px solid #999';
                cell.style.textAlign = 'center';
                cell.style.verticalAlign = 'middle';
                cell.style.cursor = 'pointer';

                if (grid[r][c].isRevealed) {
                    cell.style.backgroundColor = '#eee';
                    if (grid[r][c].isMine) {
                        cell.innerText = '💣';
                    } else if (grid[r][c].adjacentMines > 0) {
                        cell.innerText = grid[r][c].adjacentMines;
                    }
                }

                cell.addEventListener('click', () => revealCell(r, c));
                row.appendChild(cell);
            }
        }
    }

    function revealCell(r, c) {
        if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c].isRevealed) return;

        grid[r][c].isRevealed = true;
        revealedCount++;

        if (grid[r][c].isMine) {
            alert('Game Over!');
            return;
        }

        if (grid[r][c].adjacentMines === 0) {
            for (let dr = -1; dr <= 1; dr++) {
                for (let dc = -1; dc <= 1; dc++) {
                    revealCell(r + dr, c + dc);
                }
            }
        }

        if (revealedCount === rows * cols - mineCount) {
            alert('You Win!');
        }

        render();
    }

    initGame();
});
</script>

<style>
  #minesweeper table {
    border-spacing: 0;
  }
  #minesweeper td {
    border: 1px solid #aaa;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
  }
</style>
