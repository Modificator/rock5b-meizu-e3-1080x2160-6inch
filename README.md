# Rock5b使用meizu-e3-1080x2160

测试系统环境：
- ROCK 5B 系统镜像 (6.1 内核): [rock-5b_bookworm_kde_b5](https://github.com/radxa-build/rock-5b/releases/download/rsdk-b5/rock-5b_bookworm_kde_b5.output.img.xz)
- Armbian 5B vendor 系统镜像 (6.1.115 内核): [Armbian Rock 5B](https://www.armbian.com/rock-5b/)

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
## bookworm
在 rock-5b-radxa-display-meizu-e3-6inch.dts 目录下执行 sudo rsetup  -> Overlays -> Install 3rd party overlay -> rock-5b-radxa-display-meizu-e3-6inch.dts 回车。

重启系统即可。

如果执行失败了可以参考下面的替换常量的逻辑, 然后重复上面的操作，文件记得选 `rock-5b-radxa-display-meizu-e3-6inch-gen.dts`

## Armbian
Armbian 没有 rsetup 命令，但是可以用 armbian-add-overlay， armbian-add-overlay 不支持 include 语法，所以需要把常量替换成常量代表的数据
```shell
KINC=/lib/modules/$(uname -r)/build/include

cpp -nostdinc \
  -I "$KINC" \
  -undef -x assembler-with-cpp \
  rock-5b-radxa-display-meizu-e3-6inch.dts > rock-5b-radxa-display-meizu-e3-6inch-gen.dts
```
执行完后，看看有没有没替换到的， 比如 `MIPI_DSI_MODE_NO_EOT_PACKET` bookworm 有可能会没有，需要替换成 `512` 或 `(1 << 9)`

检查完后，执行 `sudo armbian-add-overlay rock-5b-radxa-display-meizu-e3-6inch-gen.dts`

重启系统即可。

