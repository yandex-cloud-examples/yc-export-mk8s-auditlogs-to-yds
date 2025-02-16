## Экспорт аудитных логов Kubernetes в Yandex Data Streams и Kinesis Data Streams

![image](https://user-images.githubusercontent.com/85429798/186873675-1769f228-d965-406f-b917-165959755333.png)


Предварительные условия
- ✅ Кластер Managed K8s.
- ✅ Terraform.
- ✅ Альфа-флаги `LOGS_ALPHA` и `TRIGGERS_CLOUD_LOGS_ALPHA` (обратитесь в службу поддержки YC для их активации).
- ✅ [Существующие потоки Yandex Data Streams](https://cloud.yandex.ru/services/data-streams).
- ✅ Значение параметра `yds_id` (для получения данного значения зайдите в развернутый YDS и скопируйте его из вкладки **Эндпоинты**, например,
https://yds.serverless.yandexcloud.net/ru-central1/b1g3o4minpkuh10pd2rj/**etnrmbadnrson5algn3s**/stream-for-k8s-audit. В данном случае значение `yds_id` — `etnrmbadnrson5algn3s`.

##
1. При работе из России создайте файл и заполните его следующим образом для использования зеркала сети Яндекса:
    ```
    cat ~/.terraformrc
    provider_installation {
      network_mirror {
        url = "https://terraform-network-mirror.storage.yandexcloud.net/"
      }
    }
    ```
1. Заполните поля в файле `provider.tf`.
1. Заполните поля в файле `terraform.tfvars.example` (см. пример ниже).
1. Выполните следующие команды:

    ```
    terraform init
    terraform apply
    ```


Пример файла `terraform.tfvars.example`:

```
folder_id                      = "b1gvnphpkgt8oechmpo0"
cloud_id                       = "b1g3o4minpkuh10pd2rj"
cluster_name                   = "k8s-for-export"

yds_stream_name = "stream-for-k8s-audit"
yds_id = "b1g3o4minpkuh10pd2rj" 
yds_ydb_id = "etnrmbadnrson5algn3s"

```
