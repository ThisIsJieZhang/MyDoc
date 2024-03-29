```
Gradle是一个构建工具，它是用来帮助我们构建app的，构建包括编译、打包等过程。我们可以为Gradle指定构建规则，然后它就会根据我们的“命令”自动为我们构建app。Android Studio中默认就使用Gradle来完成应用的构建，除此之外我们可以用gradle的指令选择性的去构建我们所需要的app。用gradle的指令构建app，需要用到gradlew（即gradle wrapper的简写），本文对gradlew的常用指令做一个总结。

  gradlew与gradlew.bat: gradlew为Linux下的shell脚本，gradlew.bat是Windows下的批处理文件。gradlew是gradle wrapper的缩写，也就是说它对gradle的命令进行了包装，比如我们进入到指定Module目录并执行“gradlew.bat assemble”即可完成对当前Module的构建（Windows系统下）。

  gradlew使用标准格式：gradlew [option...] [task...]
其中：option表示选项，task表示任务。也可以用：gradlew [task...] [option...]，具体用哪种格式可以根据个人爱好决定。下面对gradlew的常用指令做一个说明：

gradlew -?/-h/--help：显示帮助信息，即会打印可选参数及参数说明信息；
gradlew -v/--version：版本号（会打印工程用的Gradle的版本号、Kotlin、Groovy、Ant、JVM、OS等的版本号）；
gradlew tasks --all：查看所有任务，包括缓存任务等；
gradlew clean：清除工程目录下的build文件夹；
gradlew build： 检查依赖并编译打包，debug、release环境的包都会打出来；
gradlew assemble***：编译指定的包：如Debug包（gradlew assembleDebug）、Release包（gradlew assembleRelease）、渠道包（gradlew assembleOemRelease/assembleOemDebug）、定制的版本等等；
gradlew install***：编译并安装指定的包：如Debug包（gradlew installDebug）、Release包（gradlew installOemRelease/installOemDebug）、定制的版本等等；
gradlew uninstall**：卸载已安装的指定模式的包：如Debug包（gradlew uninstallDebug）、Release包（gradlew uninstallRelease）、渠道包（gradlew uninstallOemRelease/uninstallOemDebug）、定制的版本等等；
gradlew :模块名称:dependencies，如gradlew :app:dependencies，作用：查看包依赖关系；
gradlew build -i/--info -d/--debug -s/--stacktrace：编译(build)并打印debug模式和info等级的日志及所用异常的堆栈信息(--stacktrace)；
gradlew clean build --refresh-dependencies：组合指令，清除构建(gradlew clean)并重新构建(gradlew build)，同时强制刷新依赖(gradlew --refresh-dependencies)；
gradlew --offline：离线模式，即让Gradle只使用本地cache里的依赖，如果cache中没有也不会更新依赖，而是提示编译失败；
gradlew --refresh-dependencies：强制刷新依赖，即检查依赖是否有更新比如动态版本、SHA1进行本地cache和远程仓库散列码的对比等，有更新则下载更新进行构建；使用这种方式可以避免手动删除cache；
--info：打印堆栈信息；
gradlew --daemon：守护进程，使用Gradle的守护进程构建，能够提高构建效率，如果守护进程没启动或现有的都处于忙碌状态，就启动一个守护进程；
gradlew --no-daemon：如果你已经配置为使用守护进程构建，可以使用该选项本次不用守护进程构建；
gradlew --continuous：连续构建，即任务队列中即使某个任务失败，不会终止执行，而是会继续执行下一个任务；
gradlew --parallel --parallel-threads=N：并行编译；
gradlew --configure-on-demand：按需编译。
  总结：gradlew的有些指令有简写的方式，如"gradlew --version"可以用简写方式"gradlew -v代替，"gradlew --help"可以用简写方式"gradlew -h""或gradlew -?"代替，"gradlew --no-rebuild"可以用简写方式"gradlew -a"代替，"gradlew --debug"可以用简写方式"gradlew -d"代替，"gradlew --stacktrace"可以用简写方式"gradlew -s代替等等，可以发现简写的指令只需要一个减号（“-”）开头，没有简写的指令需要用两个减号（即“--”）开头。
```
