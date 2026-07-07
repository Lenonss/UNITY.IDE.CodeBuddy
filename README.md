# CodeBuddy CN Editor for Unity

Unity 编辑器插件，用于支持 CodeBuddy CN 作为 Unity 的外部代码编辑器。

## 功能

- 自动发现 CodeBuddy CN 安装
- 生成 .csproj 和 .sln 文件以支持 IntelliSense
- 在 Unity 中双击脚本时自动用 CodeBuddy CN 打开
- 自动生成 .vscode 配置文件（settings.json、launch.json、extensions.json）

## 安装

### 方式一：通过 Git URL（推荐）

- 打开 Unity → Window → Package Manager
- 点击左上角 "+"
- 选择 "Add package from git URL"
- 输入你的 GitHub 仓库 URL，例如：
  ```
  https://github.com/你的用户名/com.unity.ide.codebuddycn.git
  ```
- 点击 Add

### 方式二：本地安装

- 将本仓库克隆到本地
- 在 Package Manager 中选择 "Add package from disk"
- 选择本仓库根目录

## 使用

安装后，前往 **Edit → Preferences → External Tools**，在 External Script Editor 下拉菜单中选择 **CodeBuddy CN**。

## 系统要求

- Unity 2019.4 或更高版本
- CodeBuddy CN 已安装

## 许可证

MIT License
