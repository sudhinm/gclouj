# bigquery

A Clojure library designed to connect to BigQuery and perform all the SQL operations easily.

## Available methods
* cell-coercions
* copy-job
* create-dataset
* create-dispositions
* create-table
* dataset
* datasets
* delete-dataset
* delete-table
* execute-job
* extract-compression
* extract-format
* extract-job
* field-value->clojure
* insert-all
* job
* load-job
* query
* query-job
* query-option
* query-results
* query-results-seq
* row-hash
* running?
* service
* successful?
* table
* table-id
* tables
* ToClojure
* user-defined-function
write-dispositions

## Usage

* Set environment variable ***GOOGLE_APPLICATION_CREDENTIALS*** as path to credentials to connect to the bigquery. You can generate the service account key file (json) from GCP Console.
> GOOGLE_APPLICATION_CREDENTIALS=/Users/pingles/gcp/credentials.json


* Add dependency in your ***project.clj*** file.
> :dependencies [[gclouj/bigquery "0.2.6.0"]]

* import the framework
> (:requre [gclouj/bigquery :as bigquery])
* Create service to perform operations
```clojure
(bigquery/service {:keys [project-id], :as options})
```
* Query
```
Executes a query. BigQuery will create a Query Job and block for the specified timeout. If the query returns within the time the results will be returned. Otherwise, results need to be retrieved separately using query-results. Status of the job can be checked using the job function, and checking completed?
```
```clojure
(query service
       query
       {:keys [max-results dry-run? max-wait-millis use-cache?
               default-dataset],
        :as query-opts})
```
* Query-results
```
Retrieves results in raw sequence for a Query job. Will throw exceptions unless Job has completed successfully. Check using job and completed? functions.
```
```clojure
(query-results service
               {:keys [project-id job-id], :as job}
               &
               {:keys [max-wait-millis], :as opts})
```
* Query-results-seq
```clojure
(query-results-seq {:keys [results schema], :as query-results})
```
```
Takes a query result and coerces the results from being raw sequences into maps according to the schema and coercing values according to their type. e.g.: converts from query results of: {:results (("500")) :schema ({:name "col" :type :integer})} into... ({"col" 500} ...)
```
* For more ducumentation, visit https://cljdoc.org/d/gclouj/bigquery/0.2.6.0/api/gclouj.bigquery

## License

Copyright © 2016 Paul Ingles

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
