# Kubernetes-Learning-Notes
K8S一些相关的学习笔记


**参考学习资料：**

1. [b站的黑马程序员视频讲解](https://www.bilibili.com/video/BV1cK4y1L7Am?p=58&spm_id_from=pageDriver%20%E9%85%8D%E5%A5%97%E7%9A%84%E6%96%87%E6%A1%A3%E9%98%85%E8%AF%BB%EF%BC%9Ahttps://blog.csdn.net/demon_xi/article/details/119716509)
这个具体的说明挺好的，不过可以找一下对应的博客直接看文字形式更快。
2. 《Kubernetes权威指南》
这本书感觉稍微有点点老，大概的看一下整体框架了解一下可以，据说有新的出了。
3. [K8S官网文档](https://kubernetes.io/zh/docs/concepts)
个人认为这个最重要，理解框架的开始，里面的相关组件也说得很清楚。有问题的时候也会看这个。另外k8s这个里面还专门讲了关于集群排错等等问题，还有支持接口的插件选取等等。非常重要！！！
4. [当k8s创建pod时，背后发生了什么](https://arthurchiao.art/blog/what-happens-when-k8s-creates-pods-1-zh/)
是一个源码走读，写得还不错。
5. [关于如何理解k8s的一些概念](https://zhuanlan.zhihu.com/p/105006577)
一个知乎专栏，里面简单的说了一些k8s概念理解相关的内容，比较简短，很适合理解。
6. [k8s的对象删除机制](https://zhuanlan.zhihu.com/p/161072336)
这边写到了关于k8s对象是如何删除的，一个知乎专栏，写得还行。其实可以从这个删除的内容里，了解到一部分同步接口和异步接口，从而去思考关于一些插件需要用到的工具选取，用API聚合还是KubeBuilder这种。
7. [docker的学习及运用](https://yeasy.gitbook.io/docker_practice/)
关于docker学习的一些内容，关于docker技术从入门到实践，不过我拿这个当作一个字典一样，有时候有些相关的内容就查一查这种。
8. [一文教你了解CSI](https://developer.aliyun.com/article/783464)
CSI这个内容，是k8s中存储不可或缺的一环，可以看一下相关的概念。
9. [KubeVirt的使用指南](https://kubevirt.io/user-guide/)
一个k8s中比较厉害的插件，可以通过它启动虚拟机等。
10. [openshift中的快照](https://cloud.redhat.com/blog/live-snapshots-in-openshift-virtualization)
这个其实就是相当于用kubevirt的接口进行快照，快照的方法和存储由后端通过csi接口提供。
11. [kubevirt的数据存储](https://iswbm.com/385.html)
明哥教程里面有很多关于k8s和kubevirt的叙述学习，可以作为参考。
12. [关于cdi是如何上传镜像到卷中的](https://kubevirt.io/2018/containerized-data-importer.html)
说到kubevirt，基本上就离不开cdi，cdi的上传是一个非常好用的东西，我们可以以上传的形式挂载对应的镜像等内容到卷里，然后在通过kubevirt创建的虚拟机，就能对卷里的内容进行引用。
13. [kubevirt是如何创建出一个win10虚拟机的](https://kubevirt.io/2020/KubeVirt-installing_Microsoft_Windows_from_an_iso.html)
通过这个对应的内容，在安装了kubevirt之后，我们可以了解一下如何创建一个对应的虚拟机，算是一个入门教程。
14. [当我们没有CSI接口对应的后端存储时，如何用本地存储创建卷等](https://docs.openshift.com/container-platform/4.9/storage/persistent_storage/persistent-storage-local.html)
其实就是openshift中教如何用本地存储创建的内容。
15. [如何使用go语言写UT测试代码](https://blog.gmem.cc/ginkgo-study-note)
学习过程中免不了需要对我们已有的代码进行测试，而LLT或者UT等测试模式一定少不了，而这个内容则是go语言关于如何学习使用UT测试的内容，非常值得一读。
16. [如何对linux虚拟机的根目录进行扩容](https://blog.csdn.net/qq_39316627/article/details/123042691)
在学习的过程中，经常会发现我们对应的虚拟机的根目录下存储不够的问题，而我们在添加完硬盘之后如何扩容，这条博客写得十分详细，可以参考。
17. [Kubernetes 上免费的容器存储及容灾备份恢复方案](https://blog.csdn.net/easylife206/article/details/121571265)
velero和restic的容灾方案，不过还不支持卷为block的类型，使用kubevirt的话暂时虚拟机还没有做好卷的适配。感兴趣的还有velero的[官网](https://velero.io/docs/v1.9/restore-hooks/)可以看看。
18. [关于libvirt的底层信息](https://libvirt.org/formatdomain.html)
这里有详细介绍很多关于libvirt底层的定义等。
19. 各种学习过程中谷歌百度的资料，对于开源的代码来说，github是一定被需要的。


关于k8s是什么这个问题，在官网里面已经有了详细的解释。其中的架构和可扩展接口等提供了非常多的方便，其中以Operator模式，衍生了许多组件，例如kubebuilder等。
针对市场的需求，kubevirt也提供了一种新模式，通过kubevirt可以创建虚拟机等。k8s的基础上加上kubevirt，实现容器和虚拟机的双重控制。

勤写笔记做总结，自己搭集群去编译代码操作，学习起来就事半功倍。
多余的记录一下关于容器运行时：

 **Container Runtime（容器运行时）**
kubelet需要通过某种进程间的调用方式如 gRPC来实现与Docker容器引擎之间的调用控制功能。
实现了Kubernetes提出的CRI接口规范（ Container Runtime Interface），可以直接接入Kubernetes中。引入了CRI接口规范后，kubelet就可以通过CRI 插件来实现容器的全生命周期控制了。

CRI接口规范主要定义了两个gRPC接口服务： ImageService和RuntimeService。其中，ImageService提供了从仓库拉取镜像、查看和移除镜像的功能；RuntimeService则负责实现Pod和容器的生命周期管理，以及与容器的交互（exec/attach/port-forward）。我们知道，Pod由一组应用容器组成，其中**包含共有的环境**和**资源约束**，这个**环境在CRI里被称为Pod Sandbox**。Container Runtime可以根据自己的内部实现来解释和实现自己的Pod Sandbox。

在启动Pod之前，kubelet调用RuntimeService.RunPodSandbox来创建Pod环境， 这一过程也包括为Pod设置网络资源（分配IP等操作），Pod Sandbox 在被激活之后，就可以独立地创建、启动、停止和删除用户业务相关的Container了，当Pod销毁时，kubelet会在停止和删除Pod Sandbox之 前首先停止和删除其中的Container。


**容器进行时是啥**：一个软件(高级别，containerd，也有其他的，低级别有两个
**软件怎么定义的**：符合CRI接口规范，可以直接接入k8s
**使用场景是啥**：一般定义的在k8s使用，上述第二段
**RuntimeClass**：要做啥 -> 在一个Kubernetes集群中配置并启用多种Container Runtime，不同类型的Pod可以选择不同特性的Container Runtime来运行，以实现资源占用或者性能、稳定性等方面的优化
具体操作有对应的runtime class类型文件，设计好handler参数的配置就行，就可以创建对应的runtimeclass资源，然后可以用Pod中的 spec.runtimeClassName字段与它进行关联。
**支持**：容器镜像的获取和存储、容器的执行和管理、存储和网络相关功能。镜像拉取及基于gRPC接口的容器CRUD封装接口
**底层**：runc，也就是libcontainerd
