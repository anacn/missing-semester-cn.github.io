---
layout: page
title: Solution-数据清洗
solution: true
---
1. 学习一下这篇简短的 [交互式正则表达式教程](https://regexone.com/).
2. 统计words文件 (`/usr/share/dict/words`) 中包含至少三个`a` 且不以`'s` 结尾的单词个数。这些单词中，出现频率前三的末尾两个字母是什么？ `sed`的 `y`命令，或者 `tr` 程序也许可以帮你解决大小写的问题。共存在多少种词尾两字母组合？还有一个很 有挑战性的问题：哪个组合从未出现过？
3. 进行原地替换听上去很有诱惑力，例如：
   `sed s/REGEX/SUBSTITUTION/ input.txt > input.txt`。但是这并不是一个明智的做法，为什么呢？还是说只有 `sed`是这样的? 查看 `man sed` 来完成这个问题

4. 找出您最近十次开机的开机时间平均数、中位数和最长时间。在Linux上需要用到 `journalctl` ，而在 macOS 上使用 `log show`。找到每次起到开始和结束时的时间戳。在Linux上类似这样操作：
   ```
   Logs begin at ...
   ```
   和
   ```
   systemd[577]: Startup finished in ...
   ```
   在 macOS 上, [查找](https://eclecticlight.co/2018/03/21/macos-unified-log-3-finding-your-way/):

   ```
   === system boot:
   ```
   和
   ```
   Previous shutdown cause: 5
   ```
5. 查看之前三次重启启动信息中不同的部分(参见 `journalctl`的`-b` 选项)。将这一任务分为几个步骤，首先获取之前三次启动的启动日志，也许获取启动日志的命令就有合适的选项可以帮助您提取前三次启动的日志，亦或者您可以使用`sed '0,/STRING/d'` 来删除`STRING`匹配到的字符串前面的全部内容。然后，过滤掉每次都不相同的部分，例如时间戳。下一步，重复记录输入行并对其计数(可以使用`uniq` )。最后，删除所有出现过3次的内容（因为这些内容上三次启动日志中的重复部分）。
6. 在网上找一个类似 [这个](https://stats.wikimedia.org/EN/TablesWikipediaZZ.htm) 或者[这个](https://ucr.fbi.gov/crime-in-the-u.s/2016/crime-in-the-u.s.-2016/topic-pages/tables/table-1)的数据集。或者从[这里](https://www.springboard.com/blog/free-public-data-sets-data-science-project/)找一些。使用 `curl` 获取数据集并提取其中两列数据，如果您想要获取的是HTML数据，那么[`pup`](https://github.com/EricChiang/pup)可能会更有帮助。对于JSON类型的数据，可以试试[`jq`](https://stedolan.github.io/jq/)。请使用一条指令来找出其中一列的最大值和最小值，用另外一条指令计算两列之间差的总和。