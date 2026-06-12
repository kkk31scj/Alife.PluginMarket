# Alife Plugin Market

Alife 插件市场仓库，包含所有官方插件的元数据描述。

## 如何贡献插件

### 1. 创建插件项目

在你的项目中创建一个 C# 类库项目，命名规范为 `Alife.Function.{功能名}`。

插件需要满足以下条件：
- 项目输出为 DLL
- 主类需要添加 `[Module]` 特性
- 可以引用 `Alife.Framework` 中的接口和基类

### 2. 打包插件

将编译后的文件打包为 ZIP 文件，命名格式为 `{版本号}.zip`（如 `1.0.0.zip`）。

ZIP 文件内部结构要求：
- **文件直接在根目录**，不要包含外层文件夹
- 包含所有必要的 `.dll` 文件
- 可选包含 `.cs` 源文件（支持运行时编译）

### 3. 上传插件包

将 ZIP 文件上传到 [Alife.OfficialPluginStorage](https://github.com/BDFFZI/Alife.OfficialPluginStorage) 仓库：

```
Alife.OfficialPluginStorage/
  Alife.Function.{功能名}/
    1.0.0.zip
    1.1.0.zip  (后续版本)
```

### 4. 创建插件描述文件

在本仓库中创建一个 JSON 文件，命名为 `Alife.Function.{功能名}.json`：

```json
{
  "id": "Alife.Function.Example",
  "name": "示例插件",
  "description": "插件功能描述",
  "dependencies": {
    "Alife.Function.AnotherPlugin": ""
  },
  "environments": {
    "nuget": {
      "SomeNuGetPackage": ">=1.0.0"
    }
  },
  "releases": {
    "1.0.0": {
      "date": "2026-06-12",
      "note": "初始版本",
      "file": "https://github.com/BDFFZI/Alife.OfficialPluginStorage/raw/refs/heads/main/Alife.Function.Example/1.0.0.zip"
    }
  }
}
```

#### 字段说明

| 字段 | 说明 |
|------|------|
| `id` | 插件唯一标识，必须与文件夹名一致 |
| `name` | 插件显示名称 |
| `description` | 插件功能描述 |
| `dependencies` | 依赖的其他插件（可选） |
| `environments` | 运行环境依赖，如 nuget、pip（可选） |
| `releases` | 版本发布信息 |

### 5. 提交 PR

提交你的 JSON 文件到本仓库，等待审核合并。

## 本地开发测试

1. 将插件 DLL 放入 `Storage/Plugins/` 目录
2. 重启应用，插件会自动加载

## 相关仓库

- [Alife](https://github.com/BDFFZI/Alife) - 主项目
- [Alife.OfficialPluginStorage](https://github.com/BDFFZI/Alife.OfficialPluginStorage) - 插件包存储
