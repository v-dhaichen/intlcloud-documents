## Operation Scenario

This document describes how to use Tencent Cloud TKE to construct a simple Web application.

Web applications are divided into the following two parts:
- Frontend service, used to handle query and write requests from clients.
- Data storage service, which uses redis to store data written into the storage to redis-master, while read operations access redis-slave. Redis-master and redis-slave ensure data synchronization through master-slave replication.

This application is a sample provided with the kubernetes project. For more details, see <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">Guestbook App</a>.

##  Prerequisites
- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
- Create a cluster. For details on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Steps
### Creating redis-master Service
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the application is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/0192e80bccd66947eb505a18b4b536d4.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload name**: The name of the workload to be created. Here, `redis-master` is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **redis-master**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
![](https://main.qcloudimg.com/raw/f5a78647faa6096d81c682a271cc6aaf.png)
5. Set up **Containers in Pod** according to the following instructions. See the figure below:
 - **Name**: Enter the name of the container in the pod. Here, `master` is used as an example.
 - **Image**: Enter `ccr.ccs.tencentyun.com/library/redis`.
 - **Image Tag**: Enter `latest`.
 > Keep default settings for other options in this step.
 >
![](https://main.qcloudimg.com/raw/2a0c5b6a04d1458852d72eaa990712d7.png)
6. Set the number of pods. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
![](https://main.qcloudimg.com/raw/2abbedb170db5b366ab71351acde984c.png)
7. Set up the workload access according to the following instructions. See the figure below:   
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Intra-Cluster**.
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**: Select TCP protocol, and set the service port and target port to 6379. Other services can access the `master` container by using the service name `redis-master` and port 6379.
![](https://main.qcloudimg.com/raw/a70f48545734627844d495fd442985fa.png)
8. Click **Create workload** to complete the creation of the `redis-master` service.

### Creating redis-slave Service
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the service is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/e2430aa20d9215dec7a9cec2b711f3dd.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload name**: The name of the workload to be created. Here, `redis-slave` is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **redis-slave**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
![](https://main.qcloudimg.com/raw/81d945370bc248f6cec62a1674080895.png)
5. Set up **Containers in Pod** according to the following instructions. See the figure below:
 - **Name**: Enter the name of the container in the pod. Here, `slave` is used as an example.
 - **Image**: Enter `ccr.ccs.tencentyun.com/library/gb-redisslave`.
 - **Image Tag**: Enter `latest`.
 - **Environment variable**: Enter the following configuration information.
GET_HOSTS_FROM = dns
> Keep default settings for other options in this step.
>
![](https://main.qcloudimg.com/raw/b4c0c7bffc64bc9bb35a9329ff88810f.png)    
6. Set the number of pods. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
![](https://main.qcloudimg.com/raw/8f3f5be325ce11f1c6c2a6ca523386b6.png)
7. Set up the workload access according to the following instructions. See the figure below:   
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Intra-cluster**.
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**: Select TCP protocol, and set the service port and target port to 6379. Other services can access the `master` container by using the service name `redis-master` and port 6379.
![](https://main.qcloudimg.com/raw/05e2b80d381dd61ae7ba1d5dc53621eb.png)
8. Click **Create workload** to complete the creation of the `redis-slave` service.

#### Create Frontend Service
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the application is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/f2925b954bf4229e910d0b204f168aa0.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload name**: The name of the workload to be created. In this example, `frontend` is the workload name.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **frontend**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
![](https://main.qcloudimg.com/raw/f923b03293b8cda5145bdd5daf7b2f9d.png)
5. Set up **Containers in Pod** according to the following instructions. See the figure below:
 - **Name**: Enter the name of the container in the pod. Here, `frontend` is used as an example.
 - **Image**: Enter `ccr.ccs.tencentyun.com/library/gb-frontend`.
 - **Image Tag**: Enter `latest`.
 - **Environment variable**: Enter the following configuration information.
GET_HOSTS_FROM = dns
> Keep default settings for other options in this step.
>
![](https://main.qcloudimg.com/raw/30218adc64d1a80b8296d050725b96ba.png)
6. Set the number of pods. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
![](https://main.qcloudimg.com/raw/a7253584191db8dc28ddec7ef0abf992.png)
7. Set up the workload access according to the following instructions. See the figure below:   
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Via Internet**.
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**: Select TCP protocol. Set the service port and target port as 80. The user can access the `frontend` container by using a browser to access the cloud load balancer IP.
![](https://main.qcloudimg.com/raw/681d60e7a3a3100f1c054054406b4b11.png)
8. Click **Create workload** to complete the creation of the frontend service.


### Verify Web Application
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the cluster ID of the created service and select **Service** > **Service**. See the figure below:
3. Enter the service management page and copy the frontend service’s cloud load balancer IP. See the figure below:
![](https://main.qcloudimg.com/raw/74be16e7d6cd0ec6ec310a9430519090.png)
>
>- When creating the `redis-master` and `redis-slave` services, due to specifying the **Intra Cluster* access mode, the services only have a private IP and can only be accessed by other services in the cluster.
>- When creating the frontend service, because the access mode **Via Internet** was set, this service has a cloud load balancer (public IP) and a private IP, so it can be accessed by other services in the cluster and can also be accessed via public network.
>
4. When using a browser to access the cloud load balancer IP of the frontend service, it goes back the page as shown in the figure below, meaning that the frontend service can be accessed normally.
![](https://main.qcloudimg.com/raw/d168ffa008a9c91e8b0e0c2051abd5a3.png)
5. Enter any string in the input box and then click **Submit**, and you will see that the entered record has been saved and is displayed at the bottom of the page.
Refresh the browser page and access the service’s IP address again. The data that was originally entered will still be there, indicating that the entered string has been saved in redis.

### Development Practices
The following sample code is the complete code for the frontend service of Guestbook App. After frontend service receives an HTTP request, it determines whether it is a set command:
- If it is a set command, it takes the key and value in the parameters, and links it to the redis-master service. It also sets the key and value in redis-master.
- If it is not a set command, it links it to the redis-slave service, obtains the parameter key and corresponding value, and returns it to the client to display.

```php
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
require 'Predis/Autoloader.php';
Predis\Autoloader::register();
if (isset($_GET['cmd']) === true) {
  $host = 'redis-master';
  if (getenv('GET_HOSTS_FROM') == 'env') {
    $host = getenv('REDIS_MASTER_SERVICE_HOST');
  }
  header('Content-Type: application/json');
  if ($_GET['cmd'] == 'set') {
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $client->set($_GET['key'], $_GET['value']);
    print('{"message": "Updated"}');
  } else {
    $host = 'redis-slave';
    if (getenv('GET_HOSTS_FROM') == 'env') {
      $host = getenv('REDIS_SLAVE_SERVICE_HOST');
    }
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $value = $client->get($_GET['key']);
    print('{"data": "' . $value . '"}');
  }
} else {
  phpinfo();
} ?>

```


### Descriptions

- When the frontend service accesses the redis-master and redis-slave services, it connects to the **Service name and port**. The cluster comes with the DNS service, which resolves the service name into the corresponding service IP and performs cloud load balancing according to this IP.
Suppose the redis-slave service contains three pods. When accessing this service you directly connect to redis-slave and 6379. The DNS automatically resolves redis-slave as the service IP of the redis-slave service (a floating IP, similar to a cloud load balancer IP) and automatically performs cloud load balancing based on the redis-slave service IP. It then sends the request to a certain redis-slave service pod.
- Container environment variable settings:
 - **Use default setting (recommended setting)**: When the frontend container runs, if it reads the pre-set GET_HOSTS_FROM environment variable as dns, then it directly connects using the service name.
 - **Other settings**: The domain name of redis-master or redis-slave must be acquired from another environment variable.

