# Assignment-16.2

# Assignment-16.1


1) Pen down the limitations of MapReduce.

Here are some usecases where MapReduce does not work very well.

1. When you need a response fast. e.g. say < few seconds (Use stream processing, CEP etc instead)
2. Processing graphs
3. Complex algorithms - some machine learning algorithms like SVM,
4. Iterations - when you need to process data again and again. e.g. KMeans - 
use Spark
5. When map phase generate too many keys. Then sorting takes for ever
6. Joining two large data sets with complex conditions (equal case can be handled via hashing etc)
7. Stateful operations - e.g. evaluate a state machine
8. Cascading tasks one after the other - using Hive, Pig might help, but lot of overhead rereading and parsing data.


2) What is RDD? Explain few features of RDD?

RDD stands for “Resilient Distributed Dataset”. It is the fundamental data structure of Apache Spark. RDD in Apache Spark is an immutable collection of objects which computes on the different node of the cluster.

Decomposing the name RDD:

Resilient, i.e. fault-tolerant with the help of RDD lineage graph(DAG) and so able to recompute missing or damaged partitions due to node failures.
Distributed, since Data resides on multiple nodes.
Dataset represents records of the data you work with. The user can load the data set externally which can be either JSON file, CSV file, text file or database via JDBC with no specific data structure.
Hence, each and every dataset in RDD is logically partitioned across many servers so that they can be computed on different nodes of the cluster. RDDs are fault tolerant i.e. It posses self-recovery in the case of failure.

There are three ways to create RDDs in Spark such as – Data in stable storage, other RDDs, and parallelizing already existing collection in driver program. One can also operate Spark RDDs in parallel with a low-level API that offers transformations and actions. We will study these Spark RDD Operations later in this section.

Spark RDD can also be cached and manually partitioned. Caching is beneficial when we use RDD several times. And manual partitioning is important to correctly balance partitions. Generally, smaller partitions allow distributing RDD data more equally, among more executors. Hence, fewer partitions make the work easy.

Programmers can also call a persist method to indicate which RDDs they want to reuse in future operations. Spark keeps persistent RDDs in memory by default, but it can spill them to disk if there is not enough RAM. Users can also request other persistence strategies, such as storing the RDD only on disk or replicating it across machines, through flags to persist.


3) List down few Spark RDD operations and explain each of them.

3. RDD Transformation
3.1. map(func)
3.2. flatMap()
3.3. filter(func)
3.4. mapPartitions(func)
3.5. mapPartitionWithIndex()
3.6. union(dataset)
3.7. intersection(other-dataset)
3.8. distinct()
3.9. groupByKey()
3.10. reduceByKey(func, [numTasks])
3.11. sortByKey()
3.12. join()
3.13. coalesce()
4. RDD Action
4.1. count()
4.2. collect()
4.3. take(n)
4.4. top()
4.5. countByValue()
4.6. reduce()
4.7. fold()
4.8. aggregate()
4.9. foreach()
5. Conclusion


3.1. map(func)
The map function iterates over every line in RDD and split into new RDD. Using map() transformation we take in any function, and that function is applied to every element of RDD.

3.2. flatMap()
With the help of flatMap() function, to each input element, we have many elements in an output RDD. The most simple use of flatMap() is to split each input string into words.

3.3. filter(func)
Spark RDD filter() function returns a new RDD, containing only the elements that meet a predicate. It is a narrow operation because it does not shuffle data from one partition to many partitions.

3.4. mapPartitions(func)
The MapPartition converts each partition of the source RDD into many elements of the result (possibly none). In mapPartition(), the map() function is applied on each partitions simultaneously. MapPartition is like a map, but the difference is it runs separately on each partition(block) of the RDD

3.5. mapPartitionWithIndex()
It is like mapPartition; Besides mapPartition it provides func with an integer value representing the index of the partition, and the map() is applied on partition index wise one after the other.

3.6. union(dataset)
With the union() function, we get the elements of both the RDD in new RDD. The key rule of this function is that the two RDDs should be of the same type

3.7. intersection(other-dataset)
With the intersection() function, we get only the common element of both the RDD in new RDD. The key rule of this function is that the two RDDs should be of the same type.

3.8. distinct()
It returns a new dataset that contains the distinct elements of the source dataset. It is helpful to remove duplicate data.

3.9. groupByKey()
When we use groupByKey() on a dataset of (K, V) pairs, the data is shuffled according to the key value K in another RDD. In this transformation, lots of unnecessary data get to transfer over the network.


