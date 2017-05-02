##
## Spark java SVM for classification
##

NOTICE 1: Source code is taken from (based on) http://blogs.quovantis.com/image-classification-using-apache-spark-with-linear-svm/

NOTICE 2: The color-to-gray source code is from http://introcs.cs.princeton.edu/java/31datatype/GrayPicture.java

NOTICE 3: Images are from http://cswww.essex.ac.uk/mv/allfaces/faces96.zip

NOTICE 4: Make sure that spark 2.1.2-SNAPSHOT is used instead of spark 2.1.2 (check out build.sbt)

NOTICE 5: Images are already in grayscale.

This work is also based on 

	(1) https://docs.docker.com/engine/tutorials/dockervolumes

	(2) https://developers.google.com/protocol-buffers

	(3) http://findbugs.sourceforge.net

	(4) http://spark.apache.org/docs/latest/submitting-applications.html




[1] download (git clone) this source coded folder.

[2] cd downloaded-source-code-folder

[3] sudo make BIND_DIR=. shell

	wait ... wait ... then a bash shell will be ready (root@314d102b672a)


[4] root@314d102b672a:/# cd /home/spark_MLlib

[5] root@314d102b672a:/home/spark_MLlib# cd /examples/svm/classification

[6] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# sbt clean compile

[7] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# sbt clean package


[8] rroot@314d102b672a:/home/spark_MLlib/examples/svm/classification# /spark/bin/spark-submit  --class "SVM" ./target/scala-2.11/svm_2.11-1.0.jar  ./train-shuffled.csv ./train-shuffled.csv 20


	navie bayes accuracy : 0.8057971014492754
	svm accuracy : 0.7188405797101449



## [Appendix -- how to generate train.csv in grayscale from colorscale images]

[A-1] we assume that ./male and ./female directories contain only COLOR images

[A-2] root@314d102b672a:/home/spark_MLlib# cd /examples/svm/classification

[A-3] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# sbt clean compile

[A-4] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# sbt clean package

[A-5] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# /spark/bin/spark-submit --class "ImageParser"  ./target/scala-2.11/svm_2.11-1.0.jar  180x200  /home/spark_MLlib/examples/svm/classification/src/main/resources/male 1

[A-6] root@314d102b672a:/home/spark_MLlib/examples/svm/classification# /spark/bin/spark-submit --class "ImageParser"  ./target/scala-2.11/svm_2.11-1.0.jar  180x200  /home/spark_MLlib/examples/svm/classification/src/main/resources/female  0

[A-7] root@f31a28cc8307:/home/spark_MLlib/examples/svm/classification# sed r input-0.csv input-1.csv  > train.csv

[A-8] root@f31a28cc8307:/home/spark_MLlib/examples/svm/classification# shuf train.csv > train-shuffled.csv
