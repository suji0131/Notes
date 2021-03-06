# PySpark Tuts

[Source](https://www.tutorialspoint.com/pyspark/index.htm)

## Spark Overview
A real-time processing framework. It does in-memory computations to analyze data in real-time. It came into picture as Apache Hadoop MapReduce was performing batch processing only and lacked a real-time processing feature. Hence, Apache Spark was introduced as it can perform stream processing in real-time and can also take care of batch processing.

## PySpark Overview
Using PySpark, you can work with RDDs in Python programming language. PySpark offers **PySpark Shell** which links the Python API to the spark core and initializes the **Spark context**.

## SparkContext (SC)
SparkContext is the entry point to any spark functionality. When we run any Spark application, a driver program starts, which has the main function (SparkContext gets initiated here). The driver program then runs the operations inside the executors on worker nodes.

By default, PySpark has SparkContext available as ‘sc’, so creating a new SparkContext won't work.

```
class pyspark.SparkContext (
   master = None,                       # It is the URL of the cluster it connects to.
   appName = None,                      # Name of your job.
   sparkHome = None,                    # Spark installation directory
   pyFiles = None,                      # The .zip or .py files to send to the cluster and add to the PYTHONPATH.
   environment = None,                  # Worker nodes environment variables.
   batchSize = 0,                       # no of Py objects represented as a single Java object. 1=disable batching,   
                                        # 0=automatically choose the batch size based on object sizes, or -1 = unlimited batch size.
   serializer = PickleSerializer(),     # RDD serializer.
   conf = None,                         # An object of L{SparkConf} to set all the Spark properties.
   gateway = None,                      # Use an existing gateway and JVM, otherwise initializing a new JVM.
   jsc = None,                          # The JavaSparkContext instance.
   profiler_cls = <class 'pyspark.profiler.BasicProfiler'>
)
```

Among the above parameters, master and appname are mostly used. The first two lines of any PySpark program looks as shown below:
```
from pyspark import SparkContext

sc = SparkContext("local", "First App")
```
Spark automatically creates the SparkContext object named sc, when **PySpark shell starts**.

### Example
Lets count the number of lines with character 'a' or 'b' in the README.md file. For ex, if there are 5 lines in a file and 3 lines have the character 'a', then the output will be → Line with a: 3. Same will be done for character ‘b’.
```
from pyspark import SparkContext

#file to be read, README.md
logFile = "file:///home/hadoop/spark-2.1.0-bin-hadoop2.7/README.md"

sc = SparkContext("local", "first app")
logData = sc.textFile(logFile).cache()

numAs = logData.filter(lambda s: 'a' in s).count()
numBs = logData.filter(lambda s: 'b' in s).count()
print(numAs, numBs)
```
We will execute the following command in the terminal to run this Python file (app name and py file name is same). 
```
$SPARK_HOME/bin/spark-submit firstapp.py
```
