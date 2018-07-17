##从宿主机获取docker runing状态容器中非镜像默认文件
1. docker 信息存储位置可以使用docker info | grep Root Dir: 获取到,其默认路径为 /var/lib/docker/ , 根据Storage Driver类型的不同,路径下的文件结构会有不同, 这里只说aufs类型,
2. /var/lib/docker/aufs/ 储存所有数据的信息  
/var/lib/docker/aufs/diff 内部储存容器运行时新加文件  
/var/lib/docker/aufs/mnt 内部储存容器运行时默认文件和新生成文件的集合
3. /var/lib/docker/containers 储存所有running 状态的容器配置信息，以及容器的日志信息，可根据container id 进入对对应的容器文件夹内查看
4. /var/lib/docker/image 内部存储镜像相关信息，以及running 状态容器使用信息

#####在running状态的容器中创建一个新文件，如何才能在宿主机中定位到
* 使用 docker inspect ${containers_id} 获取到完整的containers id
* 在/var/lib/docker/image/aufs/layerdb/mounts/${containers_id}/ 内部可获取到一个${ID}值，该值可在/var/lib/docker/aufs/diff（mnt）/ 目录下找到对应存储数据的目录
