## Start a basic docker container with the following command:
```bash
docker run -d --name my-cont --memory 512m --cpus 1 nginx
docker ps
```
(--name sets the container name, --memory sets the memory limit, --cpus sets the cpu limit)

## To check namespace and cgroup isolation, run the following commands:
```bash
pid=$(ps aux | grep '[n]ginx' | sort -n -k 2 | head -n 1 | awk '{print $2}')
lsns -p $pid
```
(pid is calculated by finding the process id of the nginx process, then lsns is used to list the namespaces of the process)

## To check the cgroup of the process and the cgroup hierarchy, run the following commands:
```bash
cat /proc/$pid/cgroup
systemd-cgls --no-pager
```
(/proc/$pid/cgroup is used to check the cgroup of the process)
(To check the cgroup hierarchy, systemd-cgls is used to list the cgroups in a tree format)

## More cgroup commands:
```bash
cd /sys/fs/cgroup/memory/system.slice/docker-<container_id>.scope
cat memory.stat
cd /sys/fs/cgroup/cpu/system.slice/docker-<container_id>.scope
```
(check the memory usage of the container -> 512m)






