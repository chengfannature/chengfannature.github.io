# **ONOS**实用脚本

标签（空格分隔）：ONOS 脚本 

---

##**SHELL**脚本别名
下述的别名都是定义在`~/onos/tools/dev/bash_profile`
别名对应的脚本分布在以下几个地方：

 1. `/home/mininet/onos/tools/dev/bin`;
 2. `/home/mininet/onos/tools/test/bin`;
 3. `/home/mininet/onos/tools/build`;
可以使用`find ~/onos -name script_name`来查找脚本的具体路径。
 
|别名        | 命令   |  描述  |
| :--------: | :-----  | :----  |
|mci|'mvn clean install'|maven 清理和安装|
|mcis|'mvn clean install -DskipTests -Dcheckstyle.skip -U -T 1C'|maven 清理和安装，跳过测试和格式检查|
|mis|'mvn install -DskipTests -Dcheckstyle.skip -U -T 1C'|maven 安装，跳过测试和格式检查|
|ob|'onos-build'|不用到onos目录下，直接执行编译|
|obi|'onos-build -Dmaven.test.failure.ignore=true'|编译时忽略测试失败|
|obs|'onos-build-selective'|只编译有变更的工程|
|obd|'onos-build-docs'|编译java docs|
|op|'onos-package'|打包成可执行文件|
|ot|'onos-test'|只运行UT|
|ol|'onos-log'|查看远程测试机上的日志|
|ow|'onos-watch'||
|oi|'setPrimaryInstance'||
|pub|'onos-push-update-bundle'||
|tl|'$ONOS_ROOT/tools/dev/bin/onos-local-log'|监控本机的日志|
|tlo|'tl \| grep --colour=always -E -e "org.onlab\|org.onosproject"'|过滤ONOS组件相关的日志|
|ll|'less \$KARAF_LOG'|用ll命令打开日志|
|pp|'python -m json.tool'||
|docs|'open \$ONOS_ROOT/docs/target/site/apidocs/index.html'||
|gui|'onos-gui'||
|sshctl|'onos-ssh'||
|sshnet|'onos-ssh \$OCN'||





