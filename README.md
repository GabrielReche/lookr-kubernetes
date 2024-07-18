

# KOM - Ferramenta CLI de Métricas de Objetos do Kubernetes

O Kom é uma ferramenta de linha de comando escrita no Go que permite exibir métricas do Kubernetes para nós e pods. Ele fornece uma maneira fácil de monitorar o uso de recursos e identificar rapidamente problemas de desempenho em seu cluster do Kubernetes.

## Características

- Exibir métricas de uso de CPU e memória para todos os nós no cluster.
- Exibir métricas de uso de CPU e memória para todos os pods no cluster.
- Visualize Logs de pods e salve dentro da pasta komlogs
- Saída codificada por cores para fácil visualização dos níveis de uso de recursos.

### Saída Codificada por Cores

O Kom usa codificação de cores para visualizar os níveis de uso de recursos:

- O uso da CPU acima de 80% é exibido em vermelho.
- O uso da CPU entre 50% e 80% é exibido em amarelo.
- O uso da CPU abaixo de 50% é exibido em verde.
- O uso de memória acima de 80% é exibido em vermelho.
- O uso de memória entre 50% e 80% é exibido em amarelo.
- O uso de memória abaixo de 50% é exibido em verde.

## Instalação

Supondo que você tenha o Git e o Go instalados no seu sistema, aqui está o que você pode fazer:

Clone o repositório:

```bash
git clone https://github.com/miltlima/kom.git
```

Alterar para o diretório do projeto:

```bash
cd kom
```

Construa o binário:

```bash
go build
```

Isso gerará um arquivo binário chamado "kom" no diretório do projeto.

```bash
sudo mv kom /usr/local/bin
```

Agora, o binário "kom" está localizado na sua pasta bin, e você pode executá-lo a partir de qualquer janela de terminal, desde que a pasta bin esteja no PATH do seu sistema.

Salve o arquivo e reinicie o terminal ou execute a origem para aplicar as alterações:

```bash
source ~/.bashrc
```

Ou

```bash
source ~/.bash_profile
```

Agora, você deve ser capaz de executar o comando "kom" de qualquer lugar em seu terminal.


## Uso


## Nós kom

Para exibir métricas para todos os nós no cluster do Kubernetes, use o seguinte comando:

```bash
kom nodes
```

Isso mostrará uma tabela com informações sobre o uso da CPU, o uso da memória e os endereços IP de cada nó.

```bash
❯ ./kom nodes

+-------+-----------+-------------+----------------+----+-----------------------------------------------------------+
| NODE  |    IP     | CPU USAGE % | MEMORY USAGE % | H  |                      STATUS - LABELS                      |
+-------+-----------+-------------+----------------+----+-----------------------------------------------------------+
| node1 | 10.0.0.11 | 7           | 42             | 🟩 | OK, Has Labels: node-role.kubernetes.io/control-plane=,   |
|       |           |             |                |    | node.kubernetes.io/exclude-from-external-load-balancers=, |
|       |           |             |                |    | beta.kubernetes.io/arch=arm64,                            |
|       |           |             |                |    | beta.kubernetes.io/os=linux, kubernetes.io/arch=arm64,    |
|       |           |             |                |    | kubernetes.io/hostname=node1, kubernetes.io/os=linux      |
| node2 | 10.0.0.12 | 2           | 44             | 🟩 | OK, Has Labels:                                           |
|       |           |             |                |    | kubernetes.io/arch=arm64,                                 |
|       |           |             |                |    | kubernetes.io/hostname=node2,                             |
|       |           |             |                |    | kubernetes.io/os=linux,                                   |
|       |           |             |                |    | beta.kubernetes.io/arch=arm64,                            |
|       |           |             |                |    | beta.kubernetes.io/os=linux                               |
| node3 | 10.0.0.13 | 2           | 37             | 🟩 | OK, Has Labels:                                           |
|       |           |             |                |    | kubernetes.io/os=linux,                                   |
|       |           |             |                |    | beta.kubernetes.io/arch=arm64,                            |
|       |           |             |                |    | beta.kubernetes.io/os=linux,                              |
|       |           |             |                |    | kubernetes.io/arch=arm64,                                 |
|       |           |             |                |    | kubernetes.io/hostname=node3                              |
| node4 | 10.0.0.14 | 4           | 36             | 🟩 | OK, Has Labels:                                           |
|       |           |             |                |    | kubernetes.io/hostname=node4,                             |
|       |           |             |                |    | kubernetes.io/os=linux,                                   |
|       |           |             |                |    | beta.kubernetes.io/arch=arm64,                            |
|       |           |             |                |    | beta.kubernetes.io/os=linux,                              |
|       |           |             |                |    | kubernetes.io/arch=arm64                                  |
+-------+-----------+-------------+----------------+----+-----------------------------------------------------------+

```

## Kom pods

Para exibir métricas para todos os pods no cluster do Kubernetes, use o seguinte comando:

```bash
kom pods
```

Isso mostrará uma tabela com informações sobre cada nó, namespace do pod, nome, uso da CPU, uso da memória e IP.

```bash
❯ ./kom pods
+-------+-------------+--------------------------------------------------+-----------+-------------+----------------+----+
| NODE  |  NAMESPACE  |                       POD                        |  POD IP   | CPU USAGE % | MEMORY USAGE % | H  |
+-------+-------------+--------------------------------------------------+-----------+-------------+----------------+----+
| node2 | default     | build-code-deployment-68dd47875-4bt5p            | 10.36.0.1 | 0           | 0              | 🟩 |
| node2 | default     | health-check-deployment-59f4b679b-8k4pj          | 10.36.0.5 | 0           | 0              | 🟩 |
| node3 | default     | hidden-in-layers-qtst5                           | 10.44.0.1 | 0           | 0              | 🟩 |
| node2 | default     | internal-proxy-deployment-7699c5dd65-xm4tw       | 10.36.0.3 | 0           | 0              | 🟩 |
| node2 | default     | kubernetes-goat-home-deployment-7bf7785ff5-gghts | 10.36.0.2 | 0           | 0              | 🟩 |
| node4 | default     | metadata-db-648b64948f-vjvsg                     | 10.42.0.1 | 0           | 0              | 🟩 |
| node2 | default     | poor-registry-deployment-75f47d55dc-vhs9d        | 10.36.0.4 | 0           | 0              | 🟩 |
| node4 | default     | system-monitor-deployment-674bb4dc65-9wj4m       | 10.42.0.3 | 0           | 0              | 🟩 |
| node1 | kube-system | coredns-787d4945fb-4vnqj                         | 10.32.0.3 | 0           | 0              | 🟩 |
| node1 | kube-system | coredns-787d4945fb-q5r2h                         | 10.32.0.2 | 0           | 0              | 🟩 |
| node1 | kube-system | etcd-node1                                       | 10.0.0.11 | 1           | 1              | 🟩 |
| node1 | kube-system | kube-apiserver-node1                             | 10.0.0.11 | 3           | 8              | 🟩 |
| node1 | kube-system | kube-controller-manager-node1                    | 10.0.0.11 | 0           | 0              | 🟩 |
| node4 | kube-system | kube-proxy-5r278                                 | 10.0.0.14 | 0           | 0              | 🟩 |
| node3 | kube-system | kube-proxy-dzzrp                                 | 10.0.0.13 | 0           | 0              | 🟩 |
| node1 | kube-system | kube-proxy-h5wsb                                 | 10.0.0.11 | 0           | 0              | 🟩 |
| node2 | kube-system | kube-proxy-htlwv                                 | 10.0.0.12 | 0           | 0              | 🟩 |
| node1 | kube-system | kube-scheduler-node1                             | 10.0.0.11 | 0           | 0              | 🟩 |
| node4 | kube-system | metrics-server-75fcb88b7d-n2l7p                  | 10.0.0.14 | 0           | 0              | 🟩 |
| node4 | kube-system | weave-net-774l4                                  | 10.0.0.14 | 0           | 0              | 🟩 |
| node3 | kube-system | weave-net-gv6dn                                  | 10.0.0.13 | 0           | 0              | 🟩 |
| node2 | kube-system | weave-net-n6n8f                                  | 10.0.0.12 | 0           | 0              | 🟩 |
| node1 | kube-system | weave-net-sn6v9                                  | 10.0.0.11 | 0           | 0              | 🟩 |
+-------+-------------+--------------------------------------------------+-----------+-------------+----------------+----+
```

## Logs kom

O comando logs na Kom CLI permite coletar logs de um pod do Kubernetes e, opcionalmente, salvá-los em um arquivo.

```bash
kom logs <pod-name> [flags]
```

### Argumentos

`<pod-name>`: O nome do pod do qual você deseja coletar logs.

### Bandeiras

```bash
-s, --save: (Optional) (Opcional) Salve a saída em um arquivo de log. Se este sinalizador não for fornecido, os logs serão exibidos no terminal.
-o, --output <file-path>: (Opcional) Especifique o caminho do arquivo para salvar os logs. O padrão é output.log na pasta komlogs.
-n, --namespace <namespace>: (Opcional) Especifique o namespace do pod. O padrão é o padrão.
-c, --container <container-name>: (Opcional) Especifique o nome do contêiner no pod. Se não for fornecido, os logs serão coletados do primeiro contêiner do pod.
```
