# Game-of-Life-quickstart
康威生命游戏（Conway's Game of Life）是一种经典的计算机科学模拟，它可以在许多不同的平台上运行，包括 Google Colab。在 Google Colab 中运行生命游戏的一个好处是你可以使用 Python 编程语言，并利用 Colab 的云计算资源。

下面是一个基本的康威生命游戏的 Python 代码示例，你可以直接复制到 Google Colab 中运行：

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# 设置初始参数
GRID_SIZE = (10, 10)
RANDOM_FILL_PERCENTAGE = 0.2

def random_grid(width, height):
    """生成一个随机的初始格局"""
    return np.random.choice([1, 0], size=(width, height), p=[RANDOM_FILL_PERCENTAGE, 1 - RANDOM_FILL_PERCENTAGE])

def update(frameNum, img, grid):
    """更新游戏格局"""
    newGrid = grid.copy()
    for i in range(grid.shape[0]):
        for j in range(grid.shape[1]):
            total = int((grid[i, (j-1)%grid.shape[1]] + grid[i, (j+1)%grid.shape[1]] +
                         grid[(i-1)%grid.shape[0], j] + grid[(i+1)%grid.shape[0], j] +
                         grid[(i-1)%grid.shape[0], (j-1)%grid.shape[1]] + grid[(i-1)%grid.shape[0], (j+1)%grid.shape[1]] +
                         grid[(i+1)%grid.shape[0], (j-1)%grid.shape[1]] + grid[(i+1)%grid.shape[0], (j+1)%grid.shape[1]]) / 1)
            if grid[i, j]  == 1:
                if (total < 2) or (total > 3):
                    newGrid[i, j] = 0
            else:
                if total == 3:
                    newGrid[i, j] = 1
    img.set_data(newGrid)
    grid[:] = newGrid
    return img

# 设置初始格局
grid = random_grid(GRID_SIZE[0], GRID_SIZE[1])

# 设置动画
fig, ax = plt.subplots()
img = ax.imshow(grid, interpolation='nearest')
ani = animation.FuncAnimation(fig, update, fargs=(img, grid), frames=10, interval=100, save_count=50)

# 显示动画
plt.show()
```

这个代码示例创建了一个 10x10 的格子，其中大约 20% 的格子是“活”的（用 1 表示），其余是“死”的（用 0 表示）。随后它使用 matplotlib 库来动态显示游戏的每一步。

你可以根据自己的需要调整 `GRID_SIZE` 和 `RANDOM_FILL_PERCENTAGE` 参数，或者修改更新规则来探索生命游戏的不同变体。
