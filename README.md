# Rock5b使用meizu-e3-1080x2160

测试系统环境：ROCK 5B 系统镜像 (6.1 内核): [rock-5b_bookworm_kde_b5](https://github.com/radxa-build/rock-5b/releases/download/rsdk-b5/rock-5b_bookworm_kde_b5.output.img.xz)

# 1 安装触摸驱动

```
cd sec_ts
make clean && make -j4 && sudo make install
```



# 2 安装背光驱动

```
cd sgm37604a
make clean && make -j4 && sudo make install
```



# 3 配置设备树

在 rock-5b-radxa-display-meizu-e3-6inch.dts 目录下执行 sudo rsetup  -> Overlays -> Install 3rd party overlay -> rock-5b-radxa-display-meizu-e3-6inch.dts 回车。

重启系统即可。

