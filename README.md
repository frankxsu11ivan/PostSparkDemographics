# PostSparkDemographics
#Post warmup of Spark Unsolved
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "poHAnPg7ZPom"
   },
   "outputs": [],
   "source": [
    "import os\n",
    "# Find the latest version of spark 3.0  from http://www.apache.org/dist/spark/ and enter as the spark version\n",
    "# For example:\n",
    "# spark_version = 'spark-3.0.3'\n",
    "spark_version = 'spark-3.0.3'\n",
    "os.environ['SPARK_VERSION']=spark_version\n",
    "\n",
    "# Install Spark and Java\n",
    "!apt-get update\n",
    "!apt-get install openjdk-11-jdk-headless -qq > /dev/null\n",
    "!wget -q http://www.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop2.7.tgz\n",
    "!tar xf $SPARK_VERSION-bin-hadoop2.7.tgz\n",
    "!pip install -q findspark\n",
    "\n",
    "# Set Environment Variables\n",
    "os.environ[\"JAVA_HOME\"] = \"/usr/lib/jvm/java-11-openjdk-amd64\"\n",
    "os.environ[\"SPARK_HOME\"] = f\"/content/{spark_version}-bin-hadoop2.7\"\n",
    "\n",
    "# Start a SparkSession\n",
    "import findspark\n",
    "findspark.init()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Start Spark session\n",
    "from pyspark.sql import SparkSession\n",
    "spark = SparkSession.builder.appName(\"Demographics\").getOrCreate()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "HT_VAZmzZGqe"
   },
   "outputs": [],
   "source": [
    "# Read in data from S3 Buckets\n",
    "from pyspark import SparkFiles\n",
    "url = \"https://s3.amazonaws.com/dataviz-curriculum/day_1/demographics.csv\"\n",
    "spark.sparkContext.addFile(url)\n",
    "df = spark.read.csv(SparkFiles.get(\"demographics.csv\"), sep=\",\", header=True)\n",
    "\n",
    "# Show DataFrame\n",
    "df.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "vuhd0Jz_ZTbO"
   },
   "outputs": [],
   "source": [
    "# Print the column names"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "dn0OANoaZWjU"
   },
   "outputs": [],
   "source": [
    "# Print out the first 10 rows"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "8QzpRD8dZdsD"
   },
   "outputs": [],
   "source": [
    "# Select the age, height_meter, and weight_kg columns and use describe to show the summary statistics"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "ULIuI1pNZfws"
   },
   "outputs": [],
   "source": [
    "# Print the schema to see the types"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "iuFP8TEZZhfb"
   },
   "outputs": [],
   "source": [
    "# Rename the Salary column to `Salary (1k)` and show only this new column"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "colab": {},
    "colab_type": "code",
    "id": "NQyUp2OYZjRM"
   },
   "outputs": [],
   "source": [
    "# Create a new column called `Salary` where the values are the `Salary (1k)` * 1000\n",
    "# Show the columns `Salary` and `Salary (1k)`"
   ]
  }
 ],
 "metadata": {
  "colab": {
   "collapsed_sections": [],
   "name": "demographics_unsolved",
   "provenance": []
  },
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.7"
  },
  "latex_envs": {
   "LaTeX_envs_menu_present": true,
   "autoclose": false,
   "autocomplete": true,
   "bibliofile": "biblio.bib",
   "cite_by": "apalike",
   "current_citInitial": 1,
   "eqLabelWithNumbers": true,
   "eqNumInitial": 1,
   "hotkeys": {
    "equation": "Ctrl-E",
    "itemize": "Ctrl-I"
   },
   "labels_anchors": false,
   "latex_user_defs": false,
   "report_style_numbering": false,
   "user_envs_cfg": false
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
