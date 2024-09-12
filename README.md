

# MapReduce on IMDB Dataset

This project implements MapReduce to identify actors (or actresses) who have also acted as directors in the same movie title using the IMDB dataset.

## Prerequisites

1. **Input Files:**
   Ensure you have the following input files:
   - `imdb00-title-actors.csv`
   - `title.basics.tsv`
   - `title.crew.tsv`
   
   Place these files in the `inputImdb` folder inside the `IMDB-3mapper2reducer` directory.

2. **Java Development Kit (JDK):**
   - Ensure JDK 1.8 or higher is installed. You can check your Java version with `java -version`.

3. **Hadoop:**
   - Download and install Hadoop for Mac. Follow the [Hadoop installation guide for Mac](https://hadoop.apache.org/docs/stable/hadoop-on-macos.html) if you haven't already.

### Setting Up and Running Hadoop on Mac

1. **Configure Hadoop Environment:**

   Ensure that Hadoop is correctly set up and environment variables are configured. Edit your `.bash_profile` or `.zshrc` (depending on your shell) to include the Hadoop environment variables:

   ```bash
   export HADOOP_HOME=/usr/local/hadoop
   export PATH=$PATH:$HADOOP_HOME/bin
   ```

   Then, apply the changes:

   ```bash
   source ~/.bash_profile
   # or if using zsh
   source ~/.zshrc
   ```

2. **Start Hadoop Cluster:**

   Run the following commands to start the Hadoop single-node cluster:

   ```bash
   start-dfs.sh
   start-yarn.sh
   ```

3. **Check Hadoop UI:**

   Ensure the Hadoop UI is up and running by accessing the following URL in your browser:

   ```
   http://localhost:9870/dfshealth.html#tab-overview
   ```

4. **Upload Input Files to HDFS:**

   Place all input files in the `inputMapReduce` folder and upload this folder to Hadoop HDFS:

   ```bash
   hdfs dfs -copyFromLocal <folder_location>/inputMapReduce /
   ```

5. **Run the MapReduce Job:**

   Execute the MapReduce job with the following command. Replace `<project_folder>` with the path to your project folder:

   ```bash
   hadoop jar <project_folder>/target/NewProjectHadoop-0.0.1-SNAPSHOT.jar com.uta.MapperReducerMain /inputMapReduce/title.basics.tsv /inputMapReduce/imdb00-title-actors.csv /inputMapReduce/title.crew.tsv /mapreduce_output
   ```

6. **Handle Output:**

   Before running the MapReduce job, ensure that any existing output directory in HDFS is deleted:

   ```bash
   hdfs dfs -rm -r /mapreduce_output
   ```

   After the job completes, view the output:

   ```bash
   hdfs dfs -cat /mapreduce_output/part-r-00000
   ```

   To copy the output files to your local system:

   ```bash
   hdfs dfs -get /mapreduce_output/* output-distr
   ```

### Troubleshooting

- **If Hadoop UI is not accessible:** Ensure that Hadoop services are running correctly and check your network settings or firewall configurations.
- **If `hdfs dfs -cat` returns no results:** Verify that the MapReduce job completed successfully and check HDFS logs for errors.
- **Permission Issues:** Ensure you have the necessary permissions to run Hadoop commands and access the directories.

