# ACEP SW Data Pipeline Overview: GCP Bucket Event-Driven Processing For Archiving, On Line Analytical Processing, And Data Visualization.

Welcome to the Alaska Center for Energy and Power (ACEP) ASAPSW Data Pipeline repository. This repository centralizes documentation and links for a series of interconnected Google Cloud Platform (GCP) components designed to automate and streamline the processing of `.tar.gz` archives arriving in a designated GCP bucket. Beyond the initial processing, this pipeline system offers capabilities for archival storage, advanced data wrangling to shape and transform the data, and the automated generation of visualizations to offer immediate insights from the ingested data.

## Workflow Overview:

1. **Archive Arrival & Notification**:
    - A `.tar.gz` archive is uploaded to a specific GCP bucket.
    - A Cloud Function watches this bucket. Upon the arrival of a `.tar.gz` file, it broadcasts a message via Eventarc to Pub/Sub.

2. **Data Flow Extraction**:
    - A Dataflow job, which is subscribed to the Pub/Sub topic, triggers upon receiving the message. 
    - It unpacks the `.tar.gz` archive, processing its contents.

3. **Secondary Archiving & Notification**:
    - After unpacking, the Dataflow job stores the unpacked payload in a secondary GCP bucket, preserving the contents in their unpacked state.
    - Once this is completed, another message is broadcast to Pub/Sub, signaling that the next stage in the data pipeline can commence.

This design ensures a seamless, event-driven flow where each component is triggered based on specific conditions, ensuring efficient and timely processing. The original `.tar.gz` archive remains untouched in the initial bucket, serving as an immutable record, while the unpacked contents are made available for further processing in the secondary bucket.

---

### Core Repositories:

(You can now list the core repositories here, providing specific details about which component they represent in the workflow.)


## Repositories

1. [sw-cf-bq-gr-dash-gen](https://github.com/acep-uaf/sw-cf-bq-gr-dash-gen)
2. [sw-cf-bq-gr-dash-load](https://github.com/acep-uaf/sw-cf-bq-gr-dash-load)
3. [sw-cf-gcs-untar](https://github.com/acep-uaf/sw-cf-gcs-untar)
4. [sw-cf-gcs-ps-bq](https://github.com/acep-uaf/sw-cf-gcs-ps-bq)
5. [sw-cf-bq-pp](https://github.com/acep-uaf/sw-cf-bq-pp)
6. [sw-df-untar-gcs](https://github.com/acep-uaf/sw-df-untar-gcs)
