# hm-dianping（黑马点评）

> 仿大众点评的本地生活服务平台后端项目，基于 Spring Boot + Redis 构建。

## 📖 项目简介

hm-dianping 是一个仿大众点评模式的本地生活服务点评平台后端，主要用于学习 Spring Boot + Redis 在实际业务场景中的综合应用。项目涵盖商铺查询、探店笔记、优惠券秒杀、用户关注等核心功能模块。

### 核心功能

| 模块 | 功能说明 |
|------|----------|
| **用户模块** | 手机验证码登录、登出、个人信息查看 |
| **商铺模块** | 商铺 CRUD、按类型/名称分页查询 |
| **探店笔记** | 发布笔记、点赞、热门笔记排行、我的笔记 |
| **笔记评论** | 评论发布、回复 |
| **优惠券** | 普通优惠券、秒杀优惠券管理、按店铺查询 |
| **秒杀下单** | 秒杀券抢购（待完善） |
| **关注** | 用户间关注功能（待完善） |
| **文件上传** | 图片上传 |

## 🛠 技术栈

| 技术 | 版本 | 说明 |
|------|------|------|
| Java | 1.8 | 开发语言 |
| Spring Boot | 2.3.12.RELEASE | 基础框架 |
| MyBatis-Plus | 3.4.3 | ORM 框架 |
| MySQL | 5.1.47 | 关系型数据库 |
| Redis | - | 缓存 / Session 管理（Lettuce 客户端） |
| Apache Commons Pool 2 | - | Redis 连接池 |
| Hutool | 5.7.17 | Java 工具库 |
| Lombok | - | 代码简化 |

## 📁 项目结构

```
src/main/java/com/hmdp/
├── config/                     # 配置类
│   ├── MvcConfig.java          # MVC 拦截器配置
│   ├── MybatisConfig.java      # MyBatis-Plus 分页插件配置
│   └── WebExceptionAdvice.java # 全局异常处理
├── controller/                 # 控制器层
│   ├── BlogCommentsController.java  # 笔记评论接口
│   ├── BlogController.java         # 探店笔记接口
│   ├── FollowController.java       # 关注接口
│   ├── ShopController.java         # 商铺接口
│   ├── ShopTypeController.java     # 商铺类型接口
│   ├── UploadController.java       # 文件上传接口
│   ├── UserController.java         # 用户接口
│   ├── VoucherController.java      # 优惠券接口
│   └── VoucherOrderController.java # 秒杀订单接口
├── dto/                        # 数据传输对象
│   ├── LoginFormDTO.java       # 登录表单
│   ├── Result.java             # 统一返回结果
│   ├── ScrollResult.java       # 滚动分页结果
│   └── UserDTO.java            # 用户脱敏信息
├── entity/                     # 数据库实体
│   ├── Blog.java               # 探店笔记
│   ├── BlogComments.java       # 笔记评论
│   ├── Follow.java             # 关注
│   ├── SeckillVoucher.java     # 秒杀券
│   ├── Shop.java               # 商铺
│   ├── ShopType.java           # 商铺类型
│   ├── User.java               # 用户
│   ├── UserInfo.java           # 用户详情
│   ├── Voucher.java            # 优惠券
│   └── VoucherOrder.java       # 优惠券订单
├── mapper/                     # 数据访问层
├── service/                    # 业务逻辑层
│   └── impl/                   # 实现类
├── utils/                      # 工具类
│   ├── LoginInterceptor.java   # 登录拦截器
│   ├── PasswordEncoder.java    # 密码编码器
│   ├── RedisConstants.java     # Redis 常量
│   ├── RedisData.java          # Redis 数据封装
│   ├── RefreshTokenInterceptor.java # Token 刷新拦截器
│   ├── RegexPatterns.java      # 正则模式
│   ├── RegexUtils.java         # 正则工具
│   ├── SystemConstants.java    # 系统常量
│   └── UserHolder.java         # 用户上下文持有者
└── HmDianPingApplication.java  # 启动类
```

## 🗄 数据库表

| 表名 | 说明 |
|------|------|
| `tb_user` | 用户表 |
| `tb_user_info` | 用户详细信息表 |
| `tb_shop` | 商铺表 |
| `tb_shop_type` | 商铺类型表 |
| `tb_blog` | 探店笔记表 |
| `tb_blog_comments` | 笔记评论表 |
| `tb_voucher` | 优惠券表 |
| `tb_seckill_voucher` | 秒杀优惠券表 |
| `tb_voucher_order` | 优惠券订单表 |
| `tb_follow` | 用户关注表 |
| `tb_sign` | 签到表 |

## 🚀 快速开始

### 环境要求

- JDK 1.8+
- Maven 3.x
- MySQL 5.7+
- Redis

### 启动步骤

1. **克隆项目**

```bash
git clone <repository-url>
cd hm-dianping
```

2. **导入数据库**

在 MySQL 中创建数据库 `hmdp`，然后导入 `src/main/resources/db/hmdp.sql`：

```bash
mysql -u root -p hmdp < src/main/resources/db/hmdp.sql
```

3. **修改配置**

编辑 `src/main/resources/application.yaml`，根据本地环境修改 MySQL 和 Redis 配置：

```yaml
spring:
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/hmdp?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
    username: root
    password: root
  redis:
    host: your-redis-host
    port: 6379
    password: your-redis-password
```

4. **启动项目**

```bash
mvn spring-boot:run
```

或者使用 IDE 直接运行 `HmDianPingApplication` 主类。

启动成功后，服务默认运行在 `http://localhost:8081`。

## 📡 API 概览

### 用户
| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/user/code` | 发送手机验证码 |
| POST | `/user/login` | 登录 |
| POST | `/user/logout` | 登出（待完善） |
| GET | `/user/me` | 获取当前用户信息 |
| GET | `/user/info/{id}` | 查看用户详情 |

### 商铺
| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/shop/{id}` | 查询商铺详情 |
| POST | `/shop` | 新增商铺 |
| PUT | `/shop` | 更新商铺 |
| GET | `/shop/of/type?typeId=&current=` | 按类型分页查询 |
| GET | `/shop/of/name?name=&current=` | 按名称搜索 |

### 探店笔记
| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/blog` | 发布笔记 |
| PUT | `/blog/like/{id}` | 点赞笔记 |
| GET | `/blog/of/me` | 我的笔记 |
| GET | `/blog/hot` | 热门笔记 |

### 优惠券
| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/voucher` | 新增普通券 |
| POST | `/voucher/seckill` | 新增秒杀券 |
| GET | `/voucher/list/{shopId}` | 查询店铺优惠券 |

### 秒杀订单
| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/voucher-order/seckill/{id}` | 秒杀下单（待完善） |

## 📚 学习要点

本项目覆盖了以下 Spring Boot + Redis 实战知识点：

- **Session 共享**：基于 Redis 实现分布式 Session
- **缓存策略**：缓存穿透、缓存雪崩、缓存击穿的解决方案
- **分布式锁**：基于 Redis 实现秒杀场景下的并发控制
- **点赞功能**：基于 Redis Set 实现
- **关注 / 共同关注**：基于 Redis Set 实现
- **Feed 流**：基于 Redis Sorted Set 实现推送
- **附近商铺**：基于 Redis GEO 实现地理位置搜索
- **签到**：基于 Redis BitMap 实现

## 📝 待完善功能

- [ ] 秒杀下单业务完善
- [ ] 用户关注 / 取关
- [ ] 登出功能
- [ ] 签到功能
- [ ] Feed 流推送

## 📄 License

本项目仅用于学习交流目的。
