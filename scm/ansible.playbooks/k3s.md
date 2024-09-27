# Установка k3s с etcd

## Установка etcd

```bash
git clone https://github.com/etcd-io/etcd.git
cd etcd
./build.sh
export PATH="$PATH:`pwd`/bin"
etcd --version
```


## Установить скрипт

```bash
curl -sfL https://get.k3s.io | sh -

curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" INSTALL_K3S_CHANNEL=latest INSTALL_K3S_EXEC="server" sh -s -
```

чтобы установить дополнительные узлы агента и добавить их в кластер, запустите сценарий установки с переменными окружения `K3S_URL` и `K3S_TOKEN`. Вот пример, показывающий, как присоединиться к агенту:

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://myserver:6443 K3S_TOKEN=mynodetoken sh -

curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="agent --server https://k3s.example.com --token mypassword" sh -s -
```

> [!warning] ВАЖНО
> 
> У каждой машины должно быть уникальное имя хоста. Если у ваших машин нет уникальных имен хостов, передайте `K3S_NODE_NAME` переменную среды и укажите значение с допустимым и уникальным именем хоста для каждого узла.

> [!info] ПРИМЕЧАНИЕ
> Токен с сервера обычно находится по адресу `/var/lib/rancher/k3s/server/token`.
## Или отключить ufw (простой брандмауэр):

```bash
ufw disable
```

## Или сохранить ufw включенным по умолчанию, но потребуется внести следующие правила:

```bash
ufw allow 6443/tcp #apiserver
ufw allow 8472/udp
ufw allow 51820/udp
ufw allow 51821/udp
ufw allow 10250/tcp
ufw allow from 10.42.0.0/16 to any #pods
ufw allow from 10.43.0.0/16 to any #services
```

## Файл конфигурации

По умолчанию при установке будут использоваться значения, присутствующие в файле YAML, расположенном по адресу `/etc/rancher/k3s/config.yaml`.

```yaml
token: "secret"
debug: true
```

Поддерживается несколько файлов конфигурации. По умолчанию файлы конфигурации считываются из `/etc/rancher/k3s/config.yaml` и `/etc/rancher/k3s/config.yaml.d/*.yaml` в алфавитном порядке.

```yaml
# /etc/rancher/k3s/config.yaml
write-kubeconfig-mode: "0644"
cluster-init: true

# /etc/rancher/k3s/config.yaml.d/*.yaml
write-kubeconfig-mode: "0644"
# token: boop
tls-san="192.168.0.150"
# datastore-endpoint: "https://etcd-host-1:2379"
embedded-registry: true
```

`registries.yaml`

```yaml
mirrors:
  docker.io:
    endpoint:
      - "https://mirror.gcr.io/"
      - "https://dockerhub.timeweb.cloud"
```
