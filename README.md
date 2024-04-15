# Tutorial de Instalação do MinIO no Minikube

Este tutorial fornece instruções passo a passo sobre como instalar o MinIO no Minikube usando o Helm, com o chart Helm baixado localmente de um repositório personalizado.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos instalados no seu sistema:

* Minikube: Certifique-se de ter o Minikube instalado e em execução no seu ambiente de desenvolvimento.
* Helm: Versão 3.x ou superior
* Configuração do repositório Helm: Verifique se você adicionou o repositório Helm que contém o chart do MinIO.

## Passos

Siga estes passos para instalar o MinIO no Minikube usando o Helm:

1. Clonar o Repositório: Clone o repositório do tutorial para sua máquina local:

```bash
git clone https://github.com/GersonRS/tutorial-minio.git
```

2. Navegar até o Diretório do Repositório: Acesse o diretório do repositório:

```bash
cd tutorial-minio
```

3. Instalar o Chart do MinIO: Use o Helm para instalar o chart do MinIO do repositório local:

```bash
helm install minio ./minio -f values.yaml
```

Este comando instala o MinIO com o nome de release minio.
4. Verificar a Instalação: Verifique o status da instalação do MinIO:

```bash
kubectl get pods
```

Certifique-se de que os pods do MinIO estejam em execução e prontos antes de prosseguir.
5. Acessar o Console do MinIO: Obtenha acesso do console do MinIO via port-forward:

```bash
kubectl port-forward $(kubectl get pods --namespace default -l "release=minio" -o jsonpath="{.items[0].metadata.name}") 9001 --namespace default
```

Agora que o port-forward foi ativado use o [localhost:9001](http://localhost:9001) para acessar o console do MinIO em seu navegador da web. Você pode encontrar a chave de acesso e a chave secreta nos [valores](values.yaml) do chart do MinIO ou como segredos do Kubernetes.

6. Explorar o MinIO: Uma vez conectado ao console do MinIO, você pode começar a explorar e usar o MinIO para armazenamento de objetos.

## Limpeza

Para desinstalar o MinIO e excluir o release do Helm, use o seguinte comando:

```bash
helm uninstall minio
```

Isso remove a implantação do MinIO do seu cluster Minikube.

### Personalização Adicional

Sinta-se à vontade para personalizar a instalação do MinIO modificando os valores do chart do Helm ou explorando outras opções disponíveis no chart.
