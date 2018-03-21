```
docker pull jupyter/pyspark-notebook:latest
```

```
docker run -it --rm -p 8888:8888 \
--net=host --pid=host -e TINI_SUBREAPER=true \
-v /home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data:/home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data \
jupyter/pyspark-notebook start-notebook.sh --notebook-dir="/home/ubuntu/NYC_Traffic_Analysis_Using_Taxi_Data/"
```



https://github.com/jupyter/docker-stacks/wiki/Docker-Recipes
