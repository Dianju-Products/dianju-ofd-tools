# OFD文件处理工具

一个基于MCP（Model Context Protocol）的OFD文件处理工具包，提供PDF与OFD格式互转、OFD文件内容提取、OFD转图片等功能。

## 功能特性

- 📄 **PDF转OFD**：将PDF文件转换为OFD格式
- 📑 **OFD转PDF**：将OFD文件转换为PDF格式
- 🖼️ **OFD转图片**：将OFD文件转换为图片格式
- 📝 **OFD内容提取**：提取OFD文件的文本内容
- 📂 **文件分割**：将PDF文件分割为多个小文件
- 📤 **Base64编码**：将文件转换为Base64编码

## 安装方式

### 通过npm安装

```bash
npm install -g dianju-ofd-tools
```

### 本地开发安装

```bash
git clone https://github.com/your-repo/dianju-ofd-tools.git
cd dianju-ofd-tools
npm install
npm run build
```

## 使用方法

### 命令行方式

```bash
# PDF转OFD
ofd-tools pdf_to_ofd --filePath=/path/to/input.pdf

# OFD转PDF
ofd-tools ofd_to_pdf --filePath=/path/to/input.ofd

# OFD转图片
ofd-tools ofd_to_image --filePath=/path/to/input.ofd

# 提取OFD内容
ofd-tools get_ofd_content --filePath=/path/to/input.ofd

# 文件分割
ofd-tools spilt_file --filePath=/path/to/input.pdf

# 文件转Base64
ofd-tools read_file_as_base64 --filePath=/path/to/file
```

### 配置方式

#### 环境变量配置

```bash
export APP_ID=your_app_id
export APP_KEY=your_app_key
export API_URL=https://api.example.com
```

#### 命令行参数配置

```bash
ofd-tools --APP_ID=your_app_id --APP_KEY=your_app_key --API_URL=https://api.example.com pdf_to_ofd --filePath=/path/to/input.pdf
```

#### .env文件配置

创建`.env`文件：

```env
APP_ID=your_app_id
APP_KEY=your_app_key
API_URL=https://api.example.com
```

## API文档

### 工具列表

| 工具名称 | 描述 | 参数 |
|---------|------|------|
| `pdf_to_ofd` | 将PDF文件转换为OFD格式 | `filePath`: PDF文件路径 |
| `ofd_to_pdf` | 将OFD文件转换为PDF格式 | `filePath`: OFD文件路径 |
| `ofd_to_image` | 将OFD文件转换为图片 | `filePath`: OFD文件路径 |
| `get_ofd_content` | 提取OFD文件内容 | `filePath`: OFD文件路径 |
| `spilt_file` | 分割PDF文件 | `filePath`: PDF文件路径 |
| `read_file_as_base64` | 文件转Base64 | `filePath`: 文件路径 |

### 使用示例

```javascript
import { McpClient } from '@modelcontextprotocol/sdk/client/mcp.js';
import { StdioClientTransport } from '@modelcontextprotocol/sdk/client/stdio.js';

async function convertPdfToOfd() {
  const transport = new StdioClientTransport({
    command: 'npx',
    args: ['ofd-tools'],
  });

  const client = new McpClient({ transport });
  await client.connect();

  const result = await client.callTool('pdf_to_ofd', {
    filePath: '/path/to/input.pdf',
  });

  console.log('转换结果:', result);
}
```

## 开发指南

### 项目结构

```
src/
├── tools/          # 工具模块
│   ├── GetOfdContent.ts    # OFD内容提取
│   ├── OfdToImage.ts       # OFD转图片
│   ├── OfdToPdf.ts         # OFD转PDF
│   ├── PdfToOfd.ts         # PDF转OFD
│   ├── ReadFileAsBase64.ts # 文件转Base64
│   ├── SpiltFile.ts        # 文件分割
│   └── index.ts            # 工具导出
├── types/          # 类型定义
│   └── convert.ts  # 转换相关类型
├── utils/          # 工具函数
│   ├── config.ts   # 配置管理
│   ├── http-axios.ts # HTTP请求工具
│   ├── logger.ts   # 日志工具
│   ├── sign.ts     # 签名工具
│   └── index.ts    # 工具导出
├── index.ts        # 入口文件
├── server.ts       # 标准服务器
└── sse-server.ts   # SSE服务器
```

### 启动开发服务器

```bash
# 启动标准服务器
npm start

# 启动SSE服务器
npm run start:sse
```

### 构建项目

```bash
npm run build
```

### 类型检查

```bash
npm run typecheck
```

## 配置说明

### 配置项

| 配置项 | 说明 | 默认值 |
|-------|------|--------|
| `APP_ID` | 应用ID | 无 |
| `APP_KEY` | 应用密钥 | 无 |
| `API_URL` | API地址 | `https://api.example.com` |

### 配置优先级

1. 命令行参数（最高优先级）
2. 环境变量
3. `.env`文件
4. 默认值（最低优先级）

## 技术栈

- **框架**: Node.js + TypeScript
- **协议**: MCP (Model Context Protocol)
- **HTTP客户端**: Axios
- **类型验证**: Zod
- **构建工具**: TypeScript Compiler

## 许可证

MIT License

## 贡献

欢迎提交Issue和Pull Request！

## 联系方式

如有问题或建议，请通过以下方式联系：


- 邮箱: dianju@gmail.com
