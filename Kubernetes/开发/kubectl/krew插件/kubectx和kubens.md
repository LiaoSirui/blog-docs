## 多个集群的场景

多个 K8s 集群的三个常见用例是：

- 需要拥有多个内部集群来隔离应用程序运行环境。例如，开发阶段的应用程序应该部署在开发集群中，而测试阶段的应用程序应该部署在测试集群中，生产就绪的应用程序应该部署在生产集群中。这种方法限制了对生产集群的访问，并在生产集群上创建了强大的安全性。

<img title="" src=".assets/kubectx%E5%92%8Ckubens/1k47ocfZtlSUZrAUDhhmU3eiaGmicD7vVJvu4323AzRTlM5onOWKnQQTyDibFfvZ1Zt4cdcsk0fGV51dInOvTFy8w.png)

- K8s 管理员也可以创建虚拟集群。虚拟集群是从现有的 Kubernetes 集群中衍生出来的，并使用集群的资源。创建虚拟集群的好处是提高安全性并降低成本。

<img title="" src=".assets/kubectx%E5%92%8Ckubens/1k47ocfZtlSUZrAUDhhmU3eiaGmicD7vVJek1Onc72fsxamicwbib6W8127BDNgLM6ez133fv0ZV6pqGAZk1anAbsw.png)

## 管理多个 K8s 集群

K8s 命令行工具，`kubectl`允许对 K8s 集群运行管理命令对于配置

- 在目录`kubectl`中查找名为 config 的`$HOME/.kube`文件
- `KUBECONFIG`您可以通过设置环境变量或设置 `--kubeconfig` 标志来指定其他 kubeconfig 文件

官方提供的文档地址：<https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/>

### 单个配置文件

使用单个配置文件来定义`clusters`、`users`并`contexts`为所有 K8s 集群，例如：

要在不同集群之间切换，可以使用以下`kubectl`命令：

```bash
kubectl config --kubeconfig=config-demo use-context dev-frontend
```

将使用中定义的集群`dev-frontend`（即开发集群）

这种方法的问题在于，并不总是会以这种方式配置 kubeconfig 文件。如果有很多 K8s 集群，这个文件很快就会变得混乱。而且每次切换时都必须设置上下文。

### 多个配置文件

为每个集群创建一个单独的配置文件

可以使用`$KUBECONFIG`环境变量的一个很酷的功能，它允许你指定多个`kubeconfig`文件，用冒号分隔

```bash
KUBECONFIG=/$HOME/.kube/contexts/config-development:/$HOME/.kube/contexts/config-scratch
```

可以使用`kubectl config use-context <context_name>`在不同的上下文之间进行切换。这解决了允许拥有多个配置文件的问题，但仍然相当手动，因为每次重新启动终端或者如果有一个新的 kubeconfig（或删除一个旧的），必须更新那个环境变量。

## kubectx 和 kubens

- `kubectx` 是一个更快地在上下文（集群）之间切换的工具。
- `kubens` 是一个在 Kubernetes 命名空间之间轻松切换（并配置它们`kubectl`）的工具

官方 Github 仓库：

- 
- 

安装插件

```bash
kubectl krew install ctx

kubectl krew install ns
```

用法：

查看所有的 ctx

```bash
kubectl ctx
```

切换到 kubeconfig 中的另一个集群

```bash
kubectl ctx cluster-dev
```

切换回之前的集群

```bash
kubectl ctx -
```

为上下文创建别名

```bash
 kubectl ctx dublin=gke_ahmetb_europe-west1-b_dublin
```

列出所有命名空间

```bash
kubectl ns
```

更改 kubectl 上的活动命名空间

```bash
 kubectl ns kube-system
```

回到之前的命名空间

```bash
 kubectl ns -
```
