### Getting Started with ELK for Nginx Plus (JSON) Logs
This **Getting Started with ELK** example provides sample files to ingest, analyze & visualize **Nginx Plus logs obtained from its status API** using the ELK stack, i.e. Elasticsearch, Logstash and Kibana. The logs obtained from the status API are in JSON format.

##### Version
Example has been tested in following versions:
- Elasticsearch 1.7.3
- Logstash 1.5.4
- Kibana 4.1.1

### Installation & Setup
* Follow the [Installation & Setup Guide](https://github.com/elastic/examples/blob/master/Installation%20and%20Setup.md) to install and test the ELK stack (*you can skip this step if you have a working installation of the ELK stack,*)

* Run Elasticsearch & Kibana
  ```
  <path_to_elasticsearch_root_dir>/bin/elasticsearch
  <path_to_kibana_root_dir>/bin/kibana
  ```

* Check that Elasticsearch and Kibana are up and running.
  - Open `localhost:9200` in web browser -- should return status code 200
  - Open `localhost:5601` in web browser -- should display Kibana UI.

  **Note:** By default, Elasticsearch runs on port 9200, and Kibana run on ports 5601. If you changed the default ports during/after installation, change the above calls to use appropriate ports.

### Download Example Files

Download the following files in this repo to a local directory:
- `nginxplus_json_logs` - sample JSON formatted Nginx Plus logs from its status API
- `nginxplus_json_logstash.conf` - Logstash config for ingesting data into Elasticsearch
- `nginxplus_json_template.json` - template for custom mapping of fields
- `nginxplus_json_kibana.json` - config file to load prebuilt Kibana dashboard
- `nginxplus_json_status.sh` - script used to generate nginxplus_json_logs

** The JSON formatted logs used in this example were created using status API of Nginx Plus. Please refer to [Live activity monitoring with Nginx Plus](https://www.nginx.com/products/live-activity-monitoring/) for more information on how to use status API of Nginx Plus

### Run Example
##### 1. Ingest data into Elasticsearch using Logstash
* Execute the following command to load sample logs into Elasticsearch.

```shell
cd nginxplus_json_ELK_Example
cat nginxplus_json_logs | <path_to_logstash_root_dir>/bin/logstash -f nginxplus_json_logstash.conf
```

 * Verify that data is successfully indexed into Elasticsearch

  Running `http://localhost:9200/nginxplus_json_elk_example/_count` should return a response a `"count":3041`

 **Note:** Included `nginxplus_json_logstash.conf` configuration file assumes that you are running Elasticsearch on the same host as Logstash and have not changed the defaults. Modify the `host` and `cluster` settings in the `output { elasticsearch { ... } }`   section of nginxplus_json_logstash.conf, if needed.

##### 2. Visualize data in Kibana

* Access Kibana by going to `http://localhost:5601` in a web browser
* Connect Kibana to the `nginxplus_json_elk_example` index in Elasticsearch (auto-created in step 1)
    * Click the **Settings** tab >> **Indices** tab >> **Add New**. Specify `nginxplus_json_elk_example` as the index pattern name and click **Create** to define the index pattern
* Load sample dashboard into Kibana
    * Click the **Settings** tab >> **Objects** tab >> **Import**, and select `nginxplus_json_kibana.json`
<<<<<<< HEAD
* Open dashboard
    * Click on **Dashboard** tab and open `Sample Dashboard for Nginx Logs` dashboard

Voila! You should see the following dashboard. Enjoy!
![Kibana Dashboard Screenshot](https://cloud.githubusercontent.com/assets/1437560/11281194/5d18f368-8eae-11e5-81b6-7f401f0d2723.png)

### We would love your feedback!
If you found this example helpful and would like to see more such Getting Started examples for other standard formats, we would love would to hear from you. If you would like to contribute examples to this repo, we'd love that too!
