How to run codes for each task in AWS EMR.
=====================================================================================================
1. Upload the a3.jar file to HDFS then copy the jar file to the EMR.

2. Make an input directory using the codes below to store the input files:

hadoop fs -mkdir /input

3. Run the jar file with the code below:

spark-submit --class streaming.WordCount --master yarn --deploy-mode client a3.jar hdfs:///input hdfs:///output/taskA hdfs:///output/taskB hdfs:///output/taskC

4. Upload the files to be monitored individually to the console with a time interval of at least 3 seconds. For example:

hadoop fs -put (filename).txt /input

5. The output of task A is in /output/taskA-00*, task B in /output/taskB-00* and task C in /output/taskC-00*. To view the contents of each output file run the commands below depending on the task type, just be sure to change the asterisk(*) in the unique sequence number suffix to 1, 2, 3, etc. to specify the desired file output:

To view Task A:
hadoop fs -cat /output/taskA-00*/part*

To view Task B:
hadoop fs -cat /output/taskB-00*/part*

To view Task C:
hadoop fs -cat /output/taskC-00*/part*

Or to view all Tasks at once:
hadoop fs -cat /output/task*/part*