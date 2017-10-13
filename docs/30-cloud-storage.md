# Cloud storage
Cloud stoarge for spark enables you to have a persisted storage system backed by a cloud provider. Spark supports this by placing the appropriate storage jars and updating the core-site.xml file accordingly.

## Azure Storage Blobs (WASB)

Pre-built into this package is native support for connecting your Spark cluster to Azure Blob Storage (aka WASB). The required WASB jars are automatically placed in the spark cluster and the permissions are pulled from you secrests file.

To connect to your Azure Storage account, make sure that the storage fields in your *.aztk/core-site.xml* file are properly filled out.

Once you have correctly filled out the *.aztk/core-site.xml* with your storage credentials, you will be able to access your storage accounts from your Spark job.

Reading and writing to and from Azure blobs is easily achieved by using the `wasb` syntax. For example, reading a csv file using Pyspark would be:

```python
# read csv data into data
dataframe = spark.read.csv('wasbs://MY_CONTAINER@MY_STORAGE_ACCOUNt.blob.core.windows.net/MY_INPUT_DATA.csv')

# print off the first 5 rows
dataframe.show(5)

# write the csv back to storage
dataframe.write.csv('wasbs://MY_CONTAINER@MY_STORAGE_ACCOUNt.blob.core.windows.net/MY_OUTPUT_DATA.csv')
```

## Azure Data Lake (ADL)

Pre-built into this package is native support for connecting your Spark cluster to Azure Data Lake (aka ADL). The required ADL jars are automatically placed in the spark cluster and the permissions are pulled from your core-site.xml file under *.aztk/core-site.xml*.

To connect to your Azure Storage account, make sure that the storage fields in your *.aztk/core-site.xml* file are properly filled out.

Once you have correctly filled out the *.aztk/core-site.xml* with your data lake credentials, you will be able to access your ADL stroage repositories from your Spark job.

Reading and writing to and from Azure blobs is easily achieved by using the `adl` syntax. For example, reading a csv file using Pyspark would be:

```python
# read csv data into data
dataframe = spark.read.csv("adl://MY_ADL_STORAGE_ACCOUNT.azuredatalakestore.net/MY_INPUT_DATA.csv")

# print off the first 5 rows
dataframe.show(5)

# write the csv back to storage
dataframe.write.csv('adl://MY_ADL_STORAGE_ACCOUNT.azuredatalakestore.net/MY_OUTPUT_DATA.csv')
```

## Additional file system connectors

You can quickly add support for additional data repositories by adding the necessary JARS to your cluster, configuring the spark-defaults.conf and core-site.xml file  accordingly.

### Adding Jars

To add jar files to the cluster, simply add them to your local *.aztk/jars* directory. these will automatically get loaded into your cluster and placed under $SPARK_HOME/jars

### Registering Jars

To register the jars to use for storage update the *.aztk/spark-default.conf' file and add the path the the jar file(s) to the spark.jars property
```sh
spark.jars $spark_home/jars/my_jar_file_1.jar,$spark_home/jars/my_jar_file_2.jar
```

### Configurting file system

Configuring the file system requires and update to the *aztk/core-site.xml* file. Each file system is unique, but there are templates on how to add a file system for WASB and ADL as part of the default core-site.xml file in this project.
