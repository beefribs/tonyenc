## 介绍

- 一个简洁、高性能、跨平台的 PHP8 代码加密扩展，当前版本为 1.0.1
- 本次仅是在原作者源码基础上增加了对PHP8.0 PHP8.1的支持
- 原作者项目地址：https://github.com/lihancong/tonyenc


## 特点

- 简单快速，经实测，几乎不影响性能
- 兼容 OPcache、Xdebug 等其他扩展
- 兼容 Linux、macOS、Windows 等系统
- 兼容 Apache、Nginx + PHP-fpm、命令行等运行模式
- 加密算法较简单，这是出于速度考虑，但仍不易解密
- 若项目的 php 文件很多，建议只加密部分重要代码文件
- 要求 PHP >= 8.0

**加密前记得备份!!!**

## 更新
```
解决v1.0.0版本在PHP8.0+版本会导致cli模式报如下警告的问题：
PHP Warning:  Missing arginfo for tonyenc_encode() in Unknown on line 0
该版本移除对PHP7的支持，PHP7版本请使用v1.0.0
```

## 安装

编译前请在 core.h 中做如下修改:
```c
/* 这里定制你的加密特征头，不限长度，十六进制哦 */
const u_char tonyenc_header[] = {
        0x66, 0x88, 0xff, 0x4f,
        0x68, 0x86, 0x00, 0x56,
        0x11, 0x16, 0x16, 0x18,
};

/* 这里指定密钥，长一些更安全 */
const u_char tonyenc_key[] = {
        0x9f, 0x49, 0x52, 0x00,
        0x58, 0x9f, 0xff, 0x21,
        0x3e, 0xfe, 0xea, 0xfa,
        0xa6, 0x33, 0xf3, 0xc6,
};
```

#### 在 Linux、macOS 上编译
```
git clone https://gitee.com/lfveeker/tonyenc.git
cd tonyenc
phpize
./configure
make
```
将编译好的文件 tonyenc.so 加入到配置项 extension=tonyenc.so，重启 PHP 服务

## 加密

代码中的 `tonyenc.php` 是加密工具:
```bash
php tonyenc.php example.php dir/
```
这样即可加密 `example.php` 和 `dir` 目录下的所有 php 文件，PHP 在运行它们时会自动解密，够简单吧！

## 版权
原作者声明：
```
允许转载、修改、商用
这是我开发的第一个扩展，如有不足欢迎指正 :)
```
## 声明
本人仅是在原作者的源码基础上稍作修改，使其支持了PHP8版本