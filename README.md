[![](https://jitpack.io/v/whaitukay/spark-google-spreadsheets.svg)](https://jitpack.io/#whaitukay/spark-google-spreadsheets)

# THIS IS FORK

This library is written by **Katsunori Kanda** ([github.com/potix2](https://github.com/potix2)) and all prises for it should go to him.

This fork is meant to be usable in Scala 2.12 and Spark 3.2.1.

# Spark Google Spreadsheets

Google Spreadsheets datasource for [SparkSQL and DataFrames](http://spark.apache.org/docs/latest/sql-programming-guide.html)


If you don't know spreadsheetId, please read the [Introduction to the Google Sheets API v4](https://developers.google.com/sheets/guides/concepts).

## Requirements

This library supports different versions of Spark:

### Latest compatible versions

| This library | Spark Version |
| ------------ | ------------- |
| 2.0.x        | 3.2.x         |
| 0.7.x        | 3.0.1         |
| 0.6.x        | 2.3.x, 2.4.x  |
| 0.5.x        | 2.0.x         |
| 0.4.x        | 1.6.x         |

## Linking

Using SBT:

```
libraryDependencies += "com.github.whaitukay" %% "spark-google-spreadsheets" % "2.0.1"
```

Using Maven:

```xml
<dependency>
  <groupId>com.github.whaitukay</groupId>
  <artifactId>spark-google-spreadsheets</artifactId>
  <version>2.0.1</version>
</dependency>
```

## SQL API

```sql
CREATE TABLE cars
USING com.github.perbeatus.spark.google.spreadsheets
OPTIONS (
    path "<spreadsheetId>/worksheet1",
    serviceAccountId "xxxxxx@developer.gserviceaccount.com",
    credentialPath "/path/to/credential.p12"
)
```

## Scala API

```scala
import org.apache.spark.sql.SQLContext

val sqlContext = new SQLContext(sc)

// Creates a DataFrame from a specified worksheet
val df = sqlContext.read.
    format("com.github.perbeatus.spark.google.spreadsheets").
    option("serviceAccountId", "xxxxxx@developer.gserviceaccount.com").
    option("credentialPath", "/path/to/credential.p12").
    load("<spreadsheetId>/worksheet1")

// Saves a DataFrame to a new worksheet
df.write.
    format("com.github.perbeatus.spark.google.spreadsheets").
    option("serviceAccountId", "xxxxxx@developer.gserviceaccount.com").
    option("credentialPath", "/path/to/credential.p12").
    save("<spreadsheetId>/newWorksheet")

```

### Using Google default application credentials

Provide authentication credentials to your application code by setting the environment variable 
`GOOGLE_APPLICATION_CREDENTIALS`. The variable should be set to the path of the service account json file.


```scala
import org.apache.spark.sql.SQLContext

val sqlContext = new SQLContext(sc)

// Creates a DataFrame from a specified worksheet
val df = sqlContext.read.
    format("com.github.perbeatus.spark.google.spreadsheets").
    load("<spreadsheetId>/worksheet1")
```

More details: https://cloud.google.com/docs/authentication/production

## License

Copyright 2016-2018, Katsunori Kanda

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
