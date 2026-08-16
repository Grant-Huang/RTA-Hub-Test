# RTA-Hub 测试日志 - 场景一

## 测试信息
- **测试场景**: 场景一：标准 10' × 12' L 型厨房
- **测试模式**: 被动式用户
- **测试日期**: 2026-08-16

## 第1轮 - 选择厨房布局

### 用户输入
- 点击 "L-shape" 按钮

### AI 回复
```
Applied the "floorplan-minimal" template as a starting point: L-shape: North 144", East 120". 
These are standard numbers, not measured — please confirm below.
Two walls meeting in an L ("North" and "East").

Great — L-shape it is, and I've got your North wall at 144" and East wall at 120" 
with the plumbing and window noted. Thanks for that.

Next quick one: Is there a gas line for the range?...
```

### Confirmation Panel 变化

| 确认项 | 状态 | 值 | 来源 |
|--------|------|-----|------|
| Kitchen shape | confirmed | L-shape | 用户输入 ✓ |
| Wall North | clarify | 144" | **模板假设 ❌** |
| Wall East | clarify | 120" | **模板假设 ❌** |
| Ceiling height | confirmed | 96" | **模板假设 ❌** |
| Plumbing on East | clarify | offset 36", width 24" | **模板假设 ❌** |
| Window on North | clarify | offset 48", width 36" | **模板假设 ❌** |
| Door on East | clarify | offset 88", width 32" | **模板假设 ❌** |

### 发现的问题

#### Critical Bug: 模板假设被当作用户输入
- **用户实际输入**: 仅 "L-shape" 一个词
- **系统确认的信息**: 7项具体参数
- **问题**: 用户从未提供 Wall North=144", Wall East=120", Ceiling height=96" 等具体尺寸
- **影响**: 模板假设值被放入 Confirmation Panel，用户若不仔细检查会被当作"已确认"信息
- **AI 行为**: 说 "Thanks for that" 仿佛用户已确认，实际上用户只选了布局类型
