查看当前cpu运行频率：

```bash
cat /proc/cpuinfo | grep -i "cpu mhz"
```

开始设置：

```bash
cpupower -c all frequency-set -g performance
# 或者
cpupower frequency-set -g performance
```

再次查看当前 cpu 运行频率，最大频率运行。

```bash
cat /proc/cpuinfo | grep -i "cpu mhz"
```
