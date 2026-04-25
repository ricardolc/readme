# cgroup no Kubernetes

Este guia mostra como verificar limites de `memory` e `cpu` no `cgroup v2` para um pod Kubernetes a partir do nó onde o pod está rodando.

## 1) Descobrir o nó do pod

```bash
kubectl get pod dotnet2-cgroup-pod -o wide
```

Saída típica:

```text
NAME                READY   STATUS    RESTARTS   AGE   IP            NODE
dotnet2-cgroup-pod  1/1     Running   0          2m    10.244.1.23   worker-node-1
```

Aqui vemos que o pod está rodando em `worker-node-1`.

## 2) Acessar o nó

```bash
ssh worker-node-1
```

## 3) Descobrir o container ID

Se o cluster usa `containerd` (padrão em Kubernetes moderno):

```bash
crictl ps | grep dotnet2-cgroup-pod
```

Saída típica:

```text
CONTAINER ID   IMAGE                                      CREATED        STATE    NAME          POD
abcd1234efgh   mcr.microsoft.com/dotnet/core/runtime:2.2  2 minutes ago  Running  dotnet2-app   dotnet2-cgroup-pod
```

O container ID neste exemplo é `abcd1234efgh`.

## 4) Verificar limites no cgroup v2

Os cgroups ficam em `/sys/fs/cgroup`.

Entre no diretório do container:

```bash
cd /sys/fs/cgroup/system.slice/containerd-abcd1234efgh.scope
```

ou ajuste o nome do escopo para `containerd-<CONTAINER_ID>.scope` conforme sua instalação.

Agora cheque os arquivos:

### Memória

```bash
cat memory.max
```

- `268435456` → 256 MB
- `max` → sem limite

### CPU

```bash
cat cpu.max
```

- `100000 100000` → limite de 1 CPU
- `max` → sem limite

## Resultado esperado

O Kubernetes aplicou corretamente os limites no kernel.

> Atenção: o .NET Core 2 pode não conseguir ler corretamente os valores em `cgroup v2`, o que pode gerar erros ou fazer com que ele ignore os limites.