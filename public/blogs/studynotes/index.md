# 第一章 Windows与Linux图形化
Windows图形化
Linux命令行也支持图形化

---

# 第二章 Linux基础命令

## 1. Linux系统目录结构
* 无盘符
* 树形结构(行为树)
* 根目录 `/`（顶级目录）//层级目录

## 2. Linux命令基础
* 命令行
* 命令
* 命令通用格式
  ```bash
  command [options] [parameter]
  ```
  例如：
  ```bash
  ls -l /home/mouning
  cp -r test1 test2
  ```

## 3. ls命令入门
`ls` //列出当前目录下的的内容

### ls命令参数和选项

* **ls参数**：
  ```bash
  ls [linux路径]
  ls /  # 根目录
  ls    # 当前工作目录home
  ```

* **ls命令的选项**：
  * `ls -a` //all的意思，列出全部文件（包含隐藏文件）
  * `ls -l` //以竖向排列的形式展示内容，以及更多信息
  * `ls -h` //以易于阅读的形式展示文件的大小（h选项要和l选项一起使用）

* **PS**：命令可以组合使用
  ```bash
  ls -l -a / # 查看根目录
  ```

## 4. cd和pwd命令
* `cd` 命令用于更改工作目录 `cd [linux路径]`
  * `cd` 更改为home工作目录
  * `cd ../` 返回上一级路径的选项
  * `cd ../..` 返回上两级路径的选项
  * `cd ~` 回到当前工作目录
* `pwd` 打印输出当前工作目录

## 5. 相对路径和绝对路径
* **绝对路径**：以根目录为起点找到目标文件夹
* **相对路径**：以当前目录为起点找到目标文件夹（相对路径更加简洁）

---

### 文件操作命令

## 6. mkdir命令
* 用于创建文件夹
* **语法**：`mkdir [-p]` 适用于创建多层级的目录体系（若都不存在文件夹，可以使用 `-p` 来创建目录）
* 只能在当前的home目录创建文件夹
* 如果在home目录外需要提高权限 `sudo su` 需要输入root密码

## 7. touch and cat and more命令
* 用于创建文件
* **语法**：`touch 新建文件名`

**查看内容命令cat和命令more**
* `cat` 加上Linux路径选项，展示全部内容
* `more` 加上Linux路径选项，可以翻页查看内容，按空格翻页，按q退出查看

## 8. cp and mv and rm 命令
* `cp` 复制文件 语法：`cp linux路径`（复制文件夹要带上 `-r`）
* `mv` 移动文件 语法：`mv 移动的文件及其文件夹 移动的地方`
  * `mv text.txt text01.txt` 改名（目标不存在则有改名的效果）
* `rm` 删除文件 语法：`rm -r -f`（`-r` 表示删除文件及其文件夹，`-f` 表示强制删除）
  * `rm -rf /` 全部格式化（危险命令）

### 通配符
* `text*`，表示以text开头的文件
* `*text`，表示以text为结尾的文件
* `*text*`，表示包含text的任何内容

### 强制删除
* 普通用户无删除提示
* root管理员有删除提示
* 使用 `su - root` 进入root模式
* 使用 `exit` 退出root模式

## 9. which and find命令
* **which** 用于查找命令的程序文件 语法：`which 要查找的命令`
* **find** 用于查找指定的文件
  1. **按文件名去搜索文件**
     语法：`find 起始绝对或者相对路径 -name "查找文件名"`
     注：可以用通配符查找相应后缀或者前缀的文件名
  2. **按大小去搜索文件**
     语法：`find 起始 -size + | -n[kMG]`
     示例：
     * `-` 和 `+` 表示大于小于关系
     * `kMG` 表示具体大小的文件
     * 查找小于10kb的文件：`find / -size -10k`
     * 查找大于100MB的文件：`find / -size +10M`
     * 查找大于1GB的文件：`find / -size +1G`

## 10. grep and wc及其管道符
* **grep** 用于文件中通过关键词过滤文件行
  语法：`grep [-n] 关键字 文件路径`
  * `-n` 表示结果中显示匹配的行的行号
  * 关键字表示过滤内容的关键字用“”包起来
  * 文件路径表示要过滤的文件路径

* **wc** 用于统计文件的行数以及单词数量
  语法：`wc [-c -m -l -w] 文件路径`
  * `-c` 表示字节数量
  * `-m` 表示统计字符数量
  * `-l` 统计行数
  * `-w` 统计单词数量

* **管道符 `|`**
  左边的参数的值填给右边的结果，将左边的值填给右边式子
  例如：`ls | grep text`
  将右边的参数里面的text文件进行过滤，查找想看的文件内容

## 11. echo and tail
* **echo** 可以在命令行里输出指定内容
  语法：`echo 想输出的内容`
  * 反引号 `` ` `` 被包围的内容会作为命令去执行 语法：\`命令行\`
  * **重定向符**：
    * `>` 将命令的结果覆盖指定的文件中
    * `>>` 将左侧命令的结果，追加指定的文件中

* **tail命令行**
  可以查看文件尾部的内容，跟踪文件的更改
  语法为：`tail [-f -num] linux路径`

## 12. vim 编辑器
* 用于Linux最基本的命令输入
* 语法：`vim 文件路径` 或 `vi 文件路径`

---

# 第三章 Linux系统管理与用户权限

## 13. root用户切换
* **切换root命令**：`su - root`
* `exit` 回到上一个用户
* **注意**：禁止长期使用root用户
* **root临时用户权限** (要获得sudo认证)：命令 `sudo 其他命令`
* **sudo认证**：
  1. `visudo` 命令
  2. 添加文本末尾添加 `[用户名] ALL= (ALL)	制表符 NOPASSWD：ALL` 按esc保存，`:wq` 退出

---

## 14. 用户及其用户组管理（需要root权限）
* **创建用户组指令**：`groupadd 用户名`
* **删除用户组指令**：`groupdel 用户组名`
* **创建用户**：
  命令：`useradd 用户组（-g） 用户的home路径（-d用于指定home目录）`
* **删除用户**（默认不删除home目录）：
  命令：`userdel （使用-r删除home目录） 用户名`
* **查看用户所属的组**：
  命令：`id 用户名`
* **修改用户所属组**：
  命令：`usermod -aG 用户组 用户名`（用于指定用户加入特殊组中）
* **查询当前系统中有哪些用户**：
  命令：`getent passwd`
* **查询当前系统中有哪些组**：
  命令：`getent group`

---

## 15. 查看权限控制信息
* `r`：可读，可用ls查看
* `w`：可写，可以增删改查
* `x`：可执行，可以更改工作目录到文件夹 如cd

### 修改权限信息（root用户）
语法：`chmod [-R] 权限 文件或文件夹`
* `-R` 表示将文件夹的所有文件权限修改为rwx
* 示例：
  `chmod u=rwx,g=rx,o=x hello.txt` 将文件权限修改为：`rwxr-x--x`
  `u` 表示user所属的用户权限，`g` 表示group组权限，`o` 表示其他用户权限
  可以使用数字来填写修改的权限
  `r` 记为4，`w` 记为2，`x` 记为1，7为全部权限rwx

### 修改权限控制（root用户）
（可以修改文件，文件夹的所属用户和用户组）
语法：`chown [-R] [用户] [：] [用户组] 文件或文件夹`
* `-R` 表示将文件夹的所有文件应用相关规则
* 示例：
  * `chown root hello.txt` 将文件所属用户改为root
  * `chown :root hello.txt` 将文件所属用户组改为root
  * `chown root : itheima hello.txt` 将文件所属用户改为root，所属用户组更改为itheima
  * `chown -R root text`，将文件所属的用户改为root，并对文件应用相关规则

---

## 16. 软件安装

### CentOS `.rpm`
1. **yum命令**
   * 语法：`yum [-y] [install|remove|search] 软件名称`
   * **注意**：
     * yum命令需要root权限，sudo提权
     * yum需联网
     * `[-y]` 自动确认，无需用户审查
   * 如：
     ```bash
     yum -y install wget
     yum search wget
     yum -y remove wget
     ```

### 补充Ubuntu系统
* **apt命令** `.deb` apt
  * 语法：`apt [-y] [install|remove|search] 软件名`
  * 如：
    ```bash
    apt -y install 名
    apt -y remove 名
    apt search 名
    ```

---

# 第四章 Linux服务与进阶命令

## 17. Linux 服务管理
* `systemctl`（命令控制软件启动）
* **语法**：
  `systemctl {start|stop|status|enable|disable} 服务名`
* **含义**：
  * `start`：启动
  * `stop`：停止
  * `status`：查看状态
  * `enable`：设置开机自启动
  * `disable`：关闭开机自启动

* **内置服务**：
  * `firewalld`：防火墙
  * `NetworkManager`：主网服务
  * `network`：副网服务
  * `sshd`：SSH 服务

---

### 安装 ntp（时间控制软件）
* **安装**：
  ```bash
  yum -y install ntp
  ```
* 使用 systemctl 启动服务，并设置开机启动。

---

### 安装 httpd
* **安装**：
  ```bash
  yum install httpd
  ```
* 安装完成后，用 systemctl 控制服务。

---

### 软链接（类似于 Windows 的快捷方式）
* **语法**：
  `ln -s 参数1 参数2`
* **说明**：
  * `-s`：创建软链接（地址必须使用绝对路径）
  * `参数1`：被链接的文件或文件夹
  * `参数2`：要创建链接的位置
* **示例**：
  `ln -s /etc/yum.conf ~/yum.conf`
  表示将 `/etc/yum.conf` 在 Home 目录创建一个快捷方式。

---

### 日期和时区
* **date 命令**
  * 查看系统时间：`date`
  * 查看指定格式：`date +格式化字符串`
  * **常用格式化字符**：

| 格式 | 含义 |
| :--- | :--- |
| `%Y` | 年 |
| `%m` | 月 |
| `%d` | 日 |
| `%H` | 小时 |
| `%M` | 分钟 |
| `%S` | 秒 |
| `%s` | 从 1970-01-01 到现在的秒数 |

---

### 修改时区（使用 root 权限）
* 删除原来的时区：
  ```bash
  rm -f /etc/localtime
  ```
* 设置中国上海时区：
  ```bash
  sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
  ```

---

### 时间自动校准（NTP）
* **安装**：
  ```bash
  yum -y install ntp
  ```
* **启动服务**：
  ```bash
  systemctl start ntpd
  ```
* **设置开机启动**：
  ```bash
  systemctl enable ntpd
  ```
* **手动校准时间（root 权限）**：
  ```bash
  sudo ntpdate -u ntp.aliyun.com
  ```

---

### IP 地址
* 查看本机 IP：`ipconfig`
* **特殊 IP**：
  * `127.0.0.1`（本地回环）
  * `0.0.0.0`

---

### 主机名
* 查看主机名：`hostname`
* 修改主机名（需要 sudo 或 root 权限）：
  ```bash
  hostnamectl set-hostname 主机名
  ```

---

### 配置主机名映射
* **Windows**：
  `C:\Windows\System32\drivers\etc\hosts`
* **步骤**：
  1. 使用管理员身份运行记事本。
  2. 在 hosts 文件中添加对应的主机名和 IP 地址。
* 这样就可以通过主机名映射 IP 地址。
* 在 FinalShell 中填写主机名即可连接对应 IP。

---

### 设置 Linux 固定 IP（VMware）
* **步骤**：
  1. **VMware 中设置**
     * 设置：IP 地址范围、网关、IP 范围
  2. **Linux 中修改配置文件**
     * 编辑：`/etc/sysconfig/network-scripts/ifconfg-ens33`
     * 修改如下：
       ```text
       IPADDR=192.168.88.130
       NETMASK=255.255.255.0
       GATEWAY=192.168.88.2
       DNS1=192.168.88.2
       ```
     * **说明**：
       * `IPADDR`：IP 地址
       * `NETMASK`：子网掩码
       * `GATEWAY`：网关（与 VMware 一致）
       * `DNS1`：DNS 服务器
  3. **重启网络**：
     ```bash
     systemctl restart network
     ```
  4. **最后执行**：`ipconfig`，即可看到 IP 已固定为：`192.168.88.130`

---

## 18. 网络请求和下载

### ping命令
* **语法**：`ping [-c num] ip或者主机名`
* **选项**：`-c + 数字` 为检查的次数，不使用 `-c`，将无限次数持续检查
* **参数**：Ip和主机名

### wget命令
* 用于下载网络文件
* **命令**：`wget [-b] url`
* **选项**：`-b` 选择后台下载，会写入日志，无 `-b` 为前台下载
* `ctrl c` 停止下载
* 例如下载Hadoop，用这个镜像：
  `https://mirrors.huaweicloud.com/apache/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz`

### curl命令（相当于浏览器去打开网站）
* 用于发送网络请求，用于下载文件和获取信息
* **语法**：`curl -o url`
* **选项**：`-o` 用于下载文件，url是下载链接，可使用此选项保存文件；无 `-o` 则为发送请求
* **参数**：url，要发起网络请求的地址

---

## 19. 端口
* **概念**：设备用于外界交流通讯的出入口分为物理端口（可见）和虚拟端口（不可见），端口可以锁定计算机上的程序进行沟通
* 例如使用端口来精确连接微信，如：连接端口50001和端口5678

### 类型
* **公认端口**：系统内置和知名程序使用（1~1023）
* **注册端口**：用于绑定自用app进行通讯（10240-49151）
* **动态端口**：不绑定程序，程序对外进行网络连接时，用于临时使用（49152~65535）

### 查看端口占用
* 使用nmap命令，先安装nmap：
  ```bash
  yum -y install nmap
  ```
  `nmap 127.0.0.1`（查看本机的端口使用情况）
* 通过netstat看指定端口的占用情况：
  语法：`netstat -anp | grep 端口号`

---

## 20. 进程
* 类似于windows的任务管理器的进程
* **通过ps命令查看进程**：
  * 命令：`ps -e -f`
  * 选项 `-e` 显示全部的进程
  * 选项 `-f` 以完全格式化的形式展示信息
  * 通过管道符对结果进行过滤

* **终止进程**：
  * 命令：`kill -9 进程id`
  * 选项 `-9` 强制关闭进程

---

## 21. 主机状态
* **使用top命令查看主机的硬件占用情况**
  * 命令：`top`
  * **选项**：
    * `-p` 只显示某个进程的信息
    * `-d` 设置刷新时间默认是5s
    * `-c` 显示产生进程的完整命令
    * `-n` 指定刷新次数
    * `-b` 以非交互式全屏运行
    * `-i` 不显示任何闲置和无用的进程
    * `-u` 查找特定用户启动的进程

* **使用 `df [-h]` 查看硬盘的使用情况**
  * 命令：`df [-h]`
  * 选项 `-h` 能更加人性化显示单位

* **使用iostat查看CPU和磁盘的相关信息**
  * 语法：`iostat -x [num1][num2]`
  * 选项 `-x`，显示更多信息
  * `num1` 刷新间隔，`num2` 刷新几次

* **使用sar命令查看网络使用相关统计信息**
  * 语法：`sar -n DEV [num1][num2]`
  * `num1` 刷新间隔，`num2` 刷新几次

---

## 22. 环境变量
* **作用**：辅助系统的运行
* 使用 `env` 命令查看环境变量
* 在环境变量中 `$` 符号用于取变量的内容
* 使用 `echo` 命令直接输出path的内容

### 设置环境变量
* **临时设置变量**：使用 `export`
  * 语法：`export 变量名=变量值`

* **永久设置环境变量**：使用 `source` 命令生效更改的配置文件变量
  * 语法：先使用 `vi ~/.bashrc` 更改变量为 `export 变量名=变量值`
  * 再使用 `source` 生效更改的文件，使用 `echo` 查看自己改后的文件

* **注意**：
  * 如果对当前用户生效，配置在 `~/.bashrc` 文件中
  * 如果对所有用户生效，配置在 `/etc/profile` 文件中

### 自定义环境变量
* 使用vim编辑器修改自定义的配置文件比如mkhhaha，加上文件内容“哈哈哈”
* **注意**：添加环境变量时，应该带上原有的环境path
  * 例如：`export PATH=$PATH:/root/myenv`
  * 如果没带上原有的环境变量则会导致原有的命令使用不了

---

## 23. Linux的文件上传和下载
* 使用finalshell的文件视图工具右击文件下载到电脑的桌面
* 如果想要将windows的文件上传到Linux则只需将文件拖动至finalshell的视图窗口

### 使用插件lrzsz
* 下载插件：`yum -y install lrzsz`
* **使用rz命令上传文件**：
  语法：直接输入 `rz`（rz上传的速度很慢一般不使用，大文件的传输一般使用拖拽）
* **使用sz命令下载文件**：
  语法：`sz 要下载的文件`
  * **注意**：文件会自动下载到桌面的fsdowload中

---

## 24. 压缩和解压
（tar文件没有太多的文件压缩效果，只是把多个文件压缩到一个文件）（要减小压缩体积可以使用gzip模式）

### 压缩
* **使用tar命令压缩文件为 `.tar`, `.gz`**
  * 语法：`tar -c -v -x -f -z -C`
  * **常见压缩的选项**：
    * `-c` 创建压缩文件
    * `-v` 显示压缩和解压过程
    * `-x` 解压格式
    * `-f` 要创建的文件
    * `-z` gzip模式不使用就是tarball格式
    * `-C` 选择解压的目的地
  * **注意**：
    * `-z` 选项如果使用要位于选项第一个
    * `-f` 选项必须要在选项最后一个
  * **tar 的常用组合为**：
    * `tar -cvf test.tar 1.txt 2.txt 3.txt`
      将 1.txt 2.txt 3.txt 压缩到 test.tar 文件内
    * `tar -zcvf test.tar.gz 1.txt 2.txt 3.txt`
      将 1.txt 2.txt 3.txt 压缩到 test.tar.gz 文件内，使用 gzip 模式

* **使用zip命令压缩(更方便省事)**
  * 语法：`zip [-r] 参数1 参数2 ... 参数N`
  * `-r`，被压缩的包含文件夹的时候，需要使用 `-r` 选项，和 rm、cp 等命令的 `-r` 效果一致
  * **示例**：
    * `zip test.zip a.txt b.txt c.txt`
      将 a.txt b.txt c.txt 压缩到 test.zip 文件内
    * `zip -r test.zip test itheima a.txt`
      将 test、itheima 两个文件夹和 a.txt 文件，压缩到 test.zip 文件内

### 解压
* **unzip 命令解压文件**
  * 使用 unzip 命令，可以方便的解压 zip 压缩包
  * **语法**：`unzip [-d] 参数`
  * `-d`，指定要解压去的位置，同 tar 的 `-C` 选项
  * **参数**，被解压的 zip 压缩包文件
  * **示例**：
    * `unzip test.zip`，将 test.zip 解压到当前目录
    * `unzip test.zip -d /home/itheima`，将 test.zip 解压到指定文件夹内（/home/itheima）

* **使用tar解压**
  * 语法：`tar -xvf test.tar` (不使用 `-c` 选项，冲突)
  * **常见压缩的选项**：
    * `-c` 创建压缩文件
    * `-v` 显示压缩和解压过程
    * `-x` 解压格式
    * `-f` 要创建的文件
    * `-z` gzip模式不使用就是tarball格式
    * `-C` 选择解压的目的地
  * **常用的 tar 解压组合有**：
    * `tar -xvf test.tar`
      解压 test.tar，将文件解压至当前目录
    * `tar -xvf test.tar -C /home/itheima`
      解压 test.tar，将文件解压至指定目录（/home/itheima）
    * `tar -zxvf test.tar.gz -C /home/itheima`
      以 Gzip 模式解压 test.tar.gz，将文件解压至指定目录（/home/itheima）
  * **注意**：
    * `-f` 选项只能在选项组合体的最后
    * `-z` 选项是gzip模式解压
    * `-C` 在压缩包最后指定要解压文件的目录
