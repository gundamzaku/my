2年前刚开始看go的时候，一直不明白go是怎么进行debug的，总以为ide里面如同c或者java一样，自带了debug工具，可以设断点查当前变量值什么的。
实际上大概是想多了，并没有完善到这种程度。

现在的话，代码写多了，如果没有合适的debug工具，始终是受到一定的制约。好在在官网介绍了一个叫gdb的工具。

那么我就按他的步骤来看一下这个gdb到底是什么样的用法吧。

首先，要安装gdb，这个就自行解决了。

接着，就要
`Pass the '-w' flag to the linker to omit the debug information`
从字面的意思看是，是用-w这个参数来达到移除debug信息的目的（估计是go自带的debug信息吧）不管了，官方让我怎么做，我就怎么做。
`go build -ldflags "-w" main.go`
