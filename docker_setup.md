docker pull jupyter/pyspark-notebook:latest

docker run -it --rm -p 8888:8888 \
--net=host --pid=host -e TINI_SUBREAPER=true \
-v /home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data:/home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data \
jupyter/pyspark-notebook start-notebook.sh --notebook-dir="/home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data/"

```python
import os
os.environ['PYSPARK_SUBMIT_ARGS'] = '--packages com.amazonaws:aws-java-sdk:1.10.34,org.apache.hadoop:hadoop-aws:2.6.0 pyspark-shell'

import pyspark
sc = pyspark.SparkContext("local[*]")

from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)

hadoopConf = sc._jsc.hadoopConfiguration()
myAccessKey = input() 
mySecretKey = input()
hadoopConf.set("fs.s3.impl", "org.apache.hadoop.fs.s3native.NativeS3FileSystem")
hadoopConf.set("fs.s3.awsAccessKeyId", myAccessKey)
hadoopConf.set("fs.s3.awsSecretAccessKey", mySecretKey)

df = sqlContext.read.parquet("s3://myBucket/myKey")
```

https://github.com/jupyter/docker-stacks/wiki/Docker-Recipes
