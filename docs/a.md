# Swagger 2.0 完整示例文档112123

本文档说明了 `swagger-2.0-complete-example.json` 文件的内容结构和涵盖的字段。

## 文件内容概览

该文件包含了 Swagger/OpenAPI 2.0 规范中定义的所有主要字段和对象类型，作为完整的参考实现。

## 1. 根级别字段

- **swagger**: 版本号 ("2.0")
- **info**: 完整的 API 元数据（包含 title, description, contact, license, version 等）
- **host**: 服务器主机名
- **basePath**: API 基础路径
- **schemes**: 传输协议数组 (http, https, ws, wss)
- **consumes**: 全局可消费的 MIME 类型
- **produces**: 全局可生产的 MIME 类型
- **paths**: 完整的路径定义
- **definitions**: 数据模型定义
- **parameters**: 可重用参数定义
- **responses**: 可重用响应定义
- **securityDefinitions**: 安全方案定义
- **security**: 全局安全要求
- **tags**: 标签定义
- **externalDocs**: 外部文档链接

## 2. Path Item 对象包含

- HTTP 方法: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
- 参数定义（path, query, header, formData, body）
- 响应（responses）
- 安全要求（security）
- consumes/produces 覆盖

## 3. Schema 对象展示

### 数据类型
- 所有数据类型: string, number, integer, boolean, array, object

### 格式化
- email, date-time, date, uuid, password, byte, binary 等

### 验证关键字
- minimum, maximum, pattern, enum, required 等

### 组合关键字
- allOf

### 高级特性
- 多态性支持: discriminator
- XML 映射: xml 对象
- readOnly 属性

## 4. Parameter 对象类型

Swagger 2.0 支持五种参数类型：

- **Path 参数**: 路径模板中的参数（必须 required: true）
- **Query 参数**: URL 查询字符串参数
- **Header 参数**: 自定义请求头
- **Body 参数**: 请求体（需要 schema，每个操作最多一个）
- **FormData 参数**: 表单数据（支持文件上传，不能与 body 参数共存）

## 5. 集合格式 (collectionFormat)

数组参数支持以下集合格式：

- **csv**: 逗号分隔 `foo,bar`
- **ssv**: 空格分隔 `foo bar`
- **tsv**: 制表符分隔 `foo\tbar`
- **pipes**: 管道符分隔 `foo|bar`
- **multi**: 多个参数实例 `foo=bar&foo=baz` (仅用于 query 和 formData)

## 6. Security Definitions

Swagger 2.0 支持的安全方案：

### basic
基本 HTTP 认证

### apiKey
API 密钥认证
- 位置: header 或 query
- 需要指定参数名称

### oauth2
OAuth 2.0 认证，支持四种流程：

- **implicit**: 隐式流程
  - 需要: authorizationUrl, scopes
- **password**: 密码流程
  - 需要: tokenUrl, scopes
- **application**: 应用流程（客户端凭证）
  - 需要: tokenUrl, scopes
- **accessCode**: 授权码流程
  - 需要: authorizationUrl, tokenUrl, scopes

## 7. 特殊功能

### 文件上传
- 使用 `type: "file"` 参数
- 必须配合 `consumes: "multipart/form-data"`
- 参数必须在 `in: "formData"`

### 表单数据
支持两种表单编码：
- `application/x-www-form-urlencoded`: 简单键值对
- `multipart/form-data`: 支持文件上传

### 模型组合和继承
- 使用 `allOf` 实现模型组合
- 使用 `discriminator` 实现多态性

### 引用对象
使用 `$ref` 引用可重用组件：
- `#/definitions/ModelName`
- `#/parameters/ParamName`
- `#/responses/ResponseName`

## 8. Swagger 2.0 与 OpenAPI 3.x 的主要区别

### 服务器配置
- **Swagger 2.0**: `host`, `basePath`, `schemes`
- **OpenAPI 3.x**: `servers` 数组（支持模板变量）

### 组件组织
- **Swagger 2.0**: 根级别的 `definitions`, `parameters`, `responses`, `securityDefinitions`
- **OpenAPI 3.x**: 统一的 `components` 对象

### 请求体
- **Swagger 2.0**: 使用 `in: "body"` 的参数
- **OpenAPI 3.x**: 独立的 `requestBody` 对象

### MIME 类型
- **Swagger 2.0**: 全局和操作级别的 `consumes`/`produces`
- **OpenAPI 3.x**: 在 `content` 对象中按媒体类型定义

### 参数位置
- **Swagger 2.0**: `query`, `header`, `path`, `formData`, `body`
- **OpenAPI 3.x**: `query`, `header`, `path`, `cookie` (body 和 formData 移到 requestBody)

### OAuth2 流程名称
- **Swagger 2.0**: `implicit`, `password`, `application`, `accessCode`
- **OpenAPI 3.x**: `implicit`, `password`, `clientCredentials`, `authorizationCode`

### 新特性 (仅 OpenAPI 3.x)
- Webhooks (3.1)
- Callbacks
- Links
- Cookie 参数
- anyOf/oneOf (仅 allOf 在 2.0)
- 多个请求/响应示例

## 9. 使用场景

此示例文件可用于：
- 学习 Swagger 2.0 规范的完整字段结构
- 维护遗留的 Swagger 2.0 API 规范
- 了解 Swagger 2.0 与 OpenAPI 3.x 的差异
- 作为迁移到 OpenAPI 3.x 的参考
- 验证工具对 Swagger 2.0 的支持
- API 设计和文档的参考实现

## 10. 迁移建议

如果您正在使用 Swagger 2.0，建议考虑迁移到 OpenAPI 3.0 或 3.1：

### 迁移收益
- 更灵活的服务器配置
- 更清晰的请求体定义
- 支持回调和 Webhooks
- 更好的示例支持
- Cookie 参数支持
- 更强大的 Schema 组合能力

### 迁移工具
可以使用以下工具辅助迁移：
- Swagger Editor 的转换功能
- swagger2openapi 命令行工具
- 各种编程语言的转换库

### 注意事项
- OAuth2 流程名称变化
- 参数和请求体的结构变化
- MIME 类型定义方式变化
- 测试转换后的规范确保功能完整
