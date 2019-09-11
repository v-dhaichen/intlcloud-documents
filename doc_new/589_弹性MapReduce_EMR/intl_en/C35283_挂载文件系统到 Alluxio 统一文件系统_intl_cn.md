## Background

Alluxio provides a unified namespace mechanism that allows other file systems to be mounted to the file system of Alluxio.
In addition, it allows upper-layer applications to use the unified namespace to access data scattered across different systems.

## Operation

Command: `bin/alluxio fs mount <alluxio-path> <source-path>`

Example 1. Mount a COS bucket to an Alluxio directory.

```
bin/alluxio fs mount --option fs.cos.access.key=<COS_SECRET_ID> \
    --option fs.cos.secret.key=<COS_SECRET_KEY> \
    --option fs.cos.region=<COS_REGION> \
    --option fs.cos.app.id=<COS_APP_ID> \
    /cos cos://<COS_BUCKET>/<COS_DATA>/
```

Configure the COS configuration information in --options.

| Configuration Item          | Description                                   |
| ----------------- | -------------------------------------- |
| fs.cos.access.key | COS scecretId                         |
| fs.cos.secret.key | COS secretKey                         |
| fs.cos.region     | COS region name such as ```ap-beijing``` |
| fs.cos.app.id     | User APPID                              |
| COS_BUCKET        | COS Bucket name                         |
| COS_DATA          | COS directory, which can be the root ```/```         |

This command mounts the COS directory (specified by cos://bucket/xxx) to the /cos directory in Alluxio. 

Example 2. Mount an HDFS directory to an Alluxio directory.

`bin/alluxio fs mount /hdfs hdfs://data`

This command mounts the /data directory of HDFS to the /hdfs subdirectory of Alluxio.

After the mount is successful, the mounted content can be viewed by running the alluxio fs ls command.

