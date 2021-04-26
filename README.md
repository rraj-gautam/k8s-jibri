# k8s-jibri
Multiple jibri instances on Kubernetes Cluster. Here 20 jibri recording instances are maintained in 4 worker nodes.

* Used 8 Cores 16 GB RAM from AWS instance type c5.2xlarge as 1 jibri takes 2 cores is the reason to use four stateful sets.  
Each node can only support maximum of 30 Loopback. By default there is only 4 cards.
* To see all the devices,
```bash
$ aplay -l
```
* If you couldn't find any card devices, then install alsa module.
```bash
$ apt install alsa-utils
```
* To increase the loopback cards,
```bash
$ lsmod | grep snd_aloop
$ echo "options snd-aloop enable=1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1 index=0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29" > cat /etc/modprobe.d/alsa-loopback.conf
$ modprobe snd_aloop
```
* Check if the module is loaded
```bash
$ lsmod | grep snd_aloop
$ aplay -l
```
### using *a(1-4)-statefulset.yaml* files for pods deployment.