---
name: CodeBuddy CN 支持改造
overview: 将当前 Unity 编辑器插件从支持 TraeCN 改为支持 CodeBuddy CN，包括创建新的安装发现类、更新 Discovery 注册、以及修改包元数据。
todos:
  - id: create-codebuddy-installation
    content: 创建 VisualStudioCodeBuddyCNInstallation.cs 实现 CodeBuddy CN 安装发现
    status: completed
  - id: modify-discovery
    content: 修改 Discovery.cs 注册 CodeBuddy CN 发现逻辑
    status: completed
    dependencies:
      - create-codebuddy-installation
  - id: update-package-config
    content: 修改 package.json 更新包名称和描述
    status: completed
  - id: cleanup-traecn
    content: 移除 TraeCN 和 Codium 相关文件
    status: completed
    dependencies:
      - modify-discovery
  - id: verify-build
    content: 验证编译和元数据文件完整性
    status: completed
    dependencies:
      - update-package-config
      - cleanup-traecn
---

## 产品概述

将当前的 Unity 编辑器插件（com.unity.ide.traeCN）从支持 TraeCN 改为支持 CodeBuddy CN，使其能够作为 Unity 的外部代码编辑器，提供 csproj 生成、自动发现安装、IntelliSense 支持等功能。

## 核心功能

- 自动发现 CodeBuddy CN 的安装位置
- 生成 .csproj 文件以支持 IntelliSense
- 在 Unity 的 External Tools 设置中显示为可选编辑器
- 支持通过 CodeBuddy CN 打开项目文件
- 创建 .vscode 配置文件（launch.json、settings.json、extensions.json）以支持调试

## 技术栈

- 语言：C#
- 平台：Unity Editor（Windows/macOS/Linux）
- 框架：Unity Package Manager (UPM)
- 架构：基于现有 Visual Studio Editor 集成模式

## 实现方案

采用与 TraeCN 相同的集成模式，通过创建新的 `VisualStudioCodeBuddyCNInstallation` 类来实现 CodeBuddy CN 的支持。该方案复用现有的项目生成、发现和集成框架，只需替换编辑器特定的发现逻辑和路径配置。

### 关键修改点

1. **新建安装类**：创建 `VisualStudioCodeBuddyCNInstallation.cs`，实现 CodeBuddy CN 的安装发现和启动逻辑
2. **修改发现注册**：在 `Discovery.cs` 中注册 CodeBuddy CN 的发现逻辑
3. **更新包配置**：修改 `package.json` 中的名称和描述

### CodeBuddy CN 安装路径

- Windows: `%LOCALAPPDATA%\Programs\CodeBuddy CN\CodeBuddy CN.exe` 或 `%PROGRAMFILES%\CodeBuddy CN\CodeBuddy CN.exe`
- macOS: `/Applications/CodeBuddy CN.app`
- Linux: `/usr/bin/codebuddy` 或 `/usr/local/bin/codebuddy`

## 实现细节

### 核心目录结构

```
Editor/
├── VisualStudioCodeBuddyCNInstallation.cs  # [NEW] CodeBuddy CN 安装发现和集成
├── Discovery.cs                            # [MODIFY] 添加 CodeBuddy CN 发现注册
├── VisualStudioCodiumInstallation.cs       # [DELETE] 移除 Codium 支持（可选）
├── VisualStudioTraeCNInstallation.cs       # [DELETE] 移除 TraeCN 支持
└── package.json                            # [MODIFY] 更新包名称和描述
```

### 性能考虑

- 安装发现使用延迟加载（AsyncOperation），不会阻塞编辑器启动
- 路径搜索使用缓存机制，避免重复文件系统访问

## Agent Extensions

无适用的扩展。