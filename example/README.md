# Example of a Working Pipeline

This directory contains an example of the working pipeline, showcased with screenshots.

---

### Contents of the directory

```
example/
├── README.md
└── screenshots
    ├── 01_mystorage_with_bonze_and_parameter.png
    ├── 02_bornze_with_old_data.png
    ├── 03_parameter_dir_content.png
    ├── 04_empty_bronze.png
    ├── 05_editing_trigger.png
    ├── 06_progress_bronze.png
    ├── 07_complete_bronze_files.png
    ├── 08_manual_batch_data_pulling.png
    ├── 09_jobs_run_successfully.png
    ├── 10_jobs_run_with_trigger_right_side.png
    ├── 11_scheduling_job_trigger.png
    ├── 12_trigger_started_to_run_the_pipeline.png
    ├── 13_partial_progress_of_the_pipeline.png
    ├── 14_trigger_job_run_completed.png
    ├── 15_pipeline_run_complete.png
    ├── 16_task_in_the_job_run_pipeline.png
    ├── 17_ddca_shared_data.png
    └── 18_shared_data_content.png

```
----

A dedicated Bronze container was created at ADLS.

![Directories at ADLS](screenshots/01_mystorage_with_bonze_and_parameter.png)

---

The Bronze directory contains the raw datasets pulled from GitHub.

![Bronze Directory Contents](screenshots/02_bornze_with_old_data.png)

The Parameters directory contains a JSON file used in Azure Data Factory to pull the batch dataset. The JSON file contains configuration data about the source and destination of the dataset.

![Parameter Directory Content](screenshots/03_parameter_dir_content.png)

---

For demonstration purposes, we cleared the dataset from Bronze, and now it is empty. We did this to show that the automatic trigger is working. 
![Empty Bronze at ADLS](screenshots/04_empty_bronze.png)

---

After clearing the folder, we scheduled the trigger to run at 12:30 PM on Sunday to capture these recordings.

![Setting Trigger Time at ADF](screenshots/05_editing_trigger.png)

---

A few seconds after the trigger started running, we checked the Bronze folder and found that some files had already been loaded.

![Some Files at Bronze ADF](screenshots/06_progress_bronze.png)

---

A couple of minutes later, the data pulling process was completed, and the Bronze directory at the ADLS container contained all the necessary files.

![Completed Bronze at ADF](screenshots/07_complete_bronze_files.png)

---

To demonstrate the possibility of running the data pulling pipeline manually, we ran (debugged) the data pulling pipeline in ADF manually. Below, you can see that the process was successful.

![Manual Data Pulling](screenshots/08_manual_batch_data_pulling.png)

---

On the Databricks side, the data ingestion layer is configured to use the access key of the ADLS data storage. The data ingestion to the Bronze layer in Databricks was done automatically. The ETL pipeline in Databricks was managed to schedule and trigger automatically. Below are some screenshots taken from the ETL pipeline.

![Pipeline Jobs](screenshots/09_jobs_run_successfully.png)

---

Here is a screenshot of the jobs with trigger details.

![Pipeline Jobs with Side Bar](screenshots/10_jobs_run_with_trigger_right_side.png)

---

For demonstration purposes, the trigger was scheduled to run on Sunday at 12:48 PM after the completion of the ADF pipeline.

![Schedule Job Trigger](screenshots/11_scheduling_job_trigger.png)

---

Here is a screenshot showing that the job started at the exact time the schedule was set to execute.

![Trigger Started Running](screenshots/12_trigger_started_to_run_the_pipeline.png)

---

While the job of the pipeline was running, we checked the task of the job. As you can see in the screenshot below, the data ingestion part was completed, and the Silver layer was in progress.

![Job in Progress](screenshots/13_partial_progress_of_the_pipeline.png)

---

Finally, the triggered job was completed successfully. 
![Triggered Job Completed Successfully](screenshots/14_trigger_job_run_completed.png)

---

And every task under the job was completed successfully. 
![Pipeline Executed Successfully](screenshots/15_pipeline_run_complete.png)

---

To show you how the tasks in the job were connected, here is a screenshot of the Silver layer task in the pipeline. It displays which notebook file and cluster were used and which task this task depends on.

![](screenshots/16_task_in_the_job_run_pipeline.png)

---

After the completion of the overall pipeline, we implemented data sharing. We created a public blob data storage container in Azure Data Storage. For ease of access, we created a public URL for the uploaded file, which enables anyone with the link to download and use the information.

![Shared Data at ADLS Container](screenshots/17_ddca_shared_data.png)

Example content of the data sharing container:
![Shared Data Content](screenshots/18_shared_data_content.png)

