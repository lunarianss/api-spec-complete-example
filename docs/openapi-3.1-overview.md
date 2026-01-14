# OpenAPI 3.1 完整示例文档

本文档说明了 `openapi-3.1-complete-example.json` 文件的内容结构和涵盖的字段。

## 文件内容概览

该文件包含了 OpenAPI 3.1.1 规范中定义的所有主要字段和对象类型，作为完整的参考实现。

## 1. 根级别字段

- **openapi**: 版本号 (3.1.1)
- **info**: 完整的 API 元数据（包含 title, summary, description, contact, license, version 等）
- **jsonSchemaDialect**: JSON Schema 方言定义
- **servers**: 多个服务器配置，包含变量
- **paths**: 完整的路径定义
- **webhooks**: Webhook 定义
- **components**: 可重用组件库
- **security**: 全局安全要求
- **tags**: 标签定义
- **externalDocs**: 外部文档链接

## 2. Path Item 对象包含

- 所有 HTTP 方法: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS, TRACE
- 参数定义（path, query, header, cookie）
- 请求体（requestBody）
- 响应（responses）
- 回调（callbacks）
- 安全要求（security）
- 服务器覆盖（servers）

## 3. Schema 对象展示

### 数据类型
- 所有数据类型: string, number, integer, boolean, array, object

### 格式化
- email, date-time, date, uuid, password, binary 等

### 验证关键字
- minimum, maximum, pattern, enum, required 等

### 组合关键字
- allOf, oneOf, anyOf

### 高级特性
- 多态性支持: discriminator
- XML 映射: xml 对象
- 内容编码: contentMediaType, contentEncoding

## 4. Components 包含

- **schemas**: 完整的数据模型定义
- **responses**: 可重用响应对象
- **parameters**: 可重用参数
- **examples**: 示例数据
- **requestBodies**: 可重用请求体
- **headers**: 可重用头部
- **securitySchemes**: 所有安全方案类型
  - apiKey
  - http (bearer, basic)
  - oauth2 (所有流程)
  - openIdConnect
  - mutualTLS
- **links**: 链接对象
- **callbacks**: 回调对象
- **pathItems**: 可重用路径项

## 5. 特殊功能

### 文件操作
- 文件上传（multipart/form-data）
- 表单编码（application/x-www-form-urlencoded）

### 参数序列化
参数序列化样式：
- simple
- form
- matrix
- label
- spaceDelimited
- pipeDelimited
- deepObject

### OAuth2 流程
- implicit: 隐式流程
- password: 密码流程
- clientCredentials: 客户端凭证流程
- authorizationCode: 授权码流程

### 其他特性
- 链接和回调机制
- 引用对象（$ref）
- Webhooks 支持

## 6. OpenAPI 3.1 特有功能

OpenAPI 3.1 与 3.0 的主要区别：

- **完整兼容 JSON Schema 2020-12**: OpenAPI 3.1 的 Schema 对象就是 JSON Schema
- **支持 Webhooks**: 新增 webhooks 字段定义异步回调
- **jsonSchemaDialect 字段**: 可以指定使用的 JSON Schema 方言
- **License 对象的 identifier 字段**: 可使用 SPDX 许可证标识符
- **Info 对象的 summary 字段**: 增加简短摘要字段
- **类型联合**: Schema 中可使用 `type: ["string", "null"]` 替代 `nullable: true`
- **const 关键字**: 支持 JSON Schema 的 const 关键字
- **$schema 和 $id**: Schema 对象可使用 JSON Schema 的元数据字段
- **contentMediaType 和 contentEncoding**: 替代 3.0 中的 format: binary/byte

## 使用场景

此示例文件可用于：
- 学习 OpenAPI 3.1 规范的完整字段结构
- 作为创建新 API 规范的模板
- 验证 OpenAPI 工具对规范的支持程度
- API 设计和文档的参考实现
