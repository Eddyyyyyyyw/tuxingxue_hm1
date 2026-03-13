# Taichi Gravity Swarm

一个使用 Taichi 库实现的 GPU 加速粒子系统模拟程序，展示了粒子对鼠标位置的实时引力响应效果。

## 项目功能

- **GPU 加速**：使用 Taichi 库充分利用 GPU 并行计算能力，实现高效的粒子模拟
- **实时交互**：粒子会实时响应鼠标位置的变化，产生引力效果
- **物理模拟**：包含速度、加速度、空气阻力和边界碰撞等物理效果
- **可配置参数**：通过配置文件调整粒子数量、引力强度、颜色等参数

## 项目结构

```
CG-Lab/
├── src/
│   └── Work0/
│       ├── config.py      # 配置参数
│       ├── physics.py     # 物理模拟核心逻辑
│       └── main.py        # 主程序入口
├── .venv/                 # 虚拟环境
├── test_taichi.py         # Taichi 测试脚本
└── README.md              # 项目说明文档
```

## 安装说明

### 1. 克隆项目

```bash
git clone <项目地址>
cd CG-Lab
```

### 2. 创建并激活虚拟环境

```bash
# 创建虚拟环境
python -m venv .venv

# 激活虚拟环境
# Windows
env\Scripts\activate
# Linux/MacOS
source .venv/bin/activate
```

### 3. 安装依赖

```bash
pip install taichi
```

## 使用方法

### 运行程序

```bash
# 使用 Python 模块方式运行
.venv\Scripts\python.exe -m src.Work0.main
```

### 交互方式

1. 程序启动后会弹出一个窗口
2. 在窗口中移动鼠标，观察粒子如何跟随鼠标移动
3. 粒子会受到鼠标的引力影响，形成动态的流动效果
4. 关闭窗口即可退出程序

## 配置选项

可以通过修改 `src/Work0/config.py` 文件来调整程序参数：

| 参数 | 描述 | 默认值 |
|------|------|--------|
| NUM_PARTICLES | 粒子总数 | 30000 |
| GRAVITY_STRENGTH | 鼠标引力强度 | 0.001 |
| DRAG_COEF | 空气阻力系数 | 0.98 |
| BOUNCE_COEF | 边界反弹能量损耗 | -0.8 |
| WINDOW_RES | 窗口分辨率 | (800, 600) |
| PARTICLE_RADIUS | 粒子绘制半径 | 1.5 |
| PARTICLE_COLOR | 粒子颜色（十六进制） | 0x00BFFF（天蓝色） |

**注意**：增加粒子数量会提高视觉效果，但可能会增加 GPU 负载，导致卡顿。如果遇到性能问题，可以适当减少 `NUM_PARTICLES` 的值。

## 技术原理

1. **GPU 加速**：使用 Taichi 库的 `@ti.kernel` 装饰器将计算任务分配到 GPU 执行
2. **粒子初始化**：在 `init_particles` 函数中，为每个粒子随机分配初始位置
3. **物理更新**：在 `update_particles` 函数中，计算每个粒子受到的引力、速度变化和边界碰撞
4. **渲染**：使用 Taichi 的 GUI 模块在窗口中绘制粒子

## 依赖项

- **Python 3.7+**：运行环境
- **Taichi**：GPU 加速计算库

## 性能优化

- **粒子数量**：根据硬件性能调整 `NUM_PARTICLES` 值
- **GPU 选择**：确保 Taichi 正确使用 GPU 加速（程序启动时会显示使用的架构）
- **窗口大小**：减小 `WINDOW_RES` 可以提高渲染速度

## 示例效果
![粒子引力交互效果](https://github.com/Eddyyyyyyyw/tuxingxue_hm1/raw/main/assets/demo.gif)
当您运行程序并移动鼠标时，会看到粒子形成类似引力场的效果，跟随鼠标移动并在边界处反弹。

## 许可证

本项目采用 MIT 许可证。
