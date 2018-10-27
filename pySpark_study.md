
# PySpark learning node

1. Follow the below link to install
    - [Quick Guide installing Apache Spark (PySpark)](https://medium.com/@loldja/installing-apache-spark-pyspark-the-missing-quick-start-guide-for-windows-ad81702ba62d)
1. Use Anaconda to run pySpark

    ```bash
    cd /c/Users/kevin/Anaconda3
    source ./Scripts/activate base
    cd /d/spark
    ./bin/pyspark.cmd
    ```

    ```python
    textFile = spark.read.text("d:\spark\README.md")
    ```
1. Try to run some PySpark code logics
    - Counting # of rows
    ```python
    textFile.count()  # Number of rows in this DataFrame
    ```

    - getting the first row
    ```python
    textFile.first()  # First row in this DataFrame
    ```
    - counting letters
    ```python
    linesWithSpark = textFile.filter(textFile.value.contains("Spark"))
    textFile.filter(textFile.value.contains("Spark")).count()  # How many lines contain "Spark"?

    from pyspark.sql.functions import *
    textFile.select(size(split(textFile.value, "\s+")).name("numWords")).agg(max(col("numWords"))).collect()
    wordCounts = textFile.select(explode(split(textFile.value, "\s+")).alias("word")).groupBy("word").count()
    wordCounts.collect()
    ```

1. Submit a Python program to PySpark:
    ```bash
    ./bin/spark-submit --master local[4] SimpleApp.py
    ```