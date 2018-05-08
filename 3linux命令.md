# bigdata
#> mv

#
> su xxx  切换了root身份，但Shell环境仍然是普通用户的Shell；  
>>su -  xxx   连用户和Shell环境一起切换成root身份了。只有切换了Shell环境才不会出现PATH环境变量错误。su切换成root用户以后，pwd
一下，发现工作目录仍然是普通用户的工作目录；而用su -命令切换以后，工作目录变成root的工作目录了

#
> /ext/profile


#
> tail  -f   根据文件描述符进行追踪，当文件改名或被删除，追踪停止
>> tail  -F  --retry，根据文件名进行追踪，并保持重试，即该文件被删除或改名后，如果再次创建相同的文件名，会继续追踪
