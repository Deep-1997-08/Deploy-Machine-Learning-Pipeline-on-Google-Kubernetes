# Intrusion Detection Framework Using the UNSW_NB15 Dataset
This project utilizes the UNSW_NB15 dataset, focusing on a comprehensive set of features for anomaly detection:

## Overview of Workflow:

The dataset, containing CSV files, serves as the foundation for our analysis. The dataset division reveals that 45% of the training set comprises normal traffic, with the remainder identified as malicious activities. The analysis is driven by a carefully selected set of features, categorized as follows:

- Categorical Features: `proto`
- Numerical Features: `dur`, `spkts`, `dpkts`, `sbytes`, `dbytes`, `rate`, `sttl`, `dttl`, `sload`, `dload`, `sloss`, `dloss`, `sinpkt`, `dinpkt`, `sjit`, `djit`, `swin`, `stcpb`, `dtcpb`, `dwin`, `tcprtt`, `synack`, `ackdat`, `smean`, `dmean`, `trans_depth`, `response_body_len`, `ct_srv_src`, `ct_state_ttl`, `ct_dst_ltm`, `ct_src_dport_ltm`, `ct_dst_sport_ltm`, `ct_dst_src_ltm`, `is_ftp_login`, `ct_ftp_cmd`, `ct_flw_http_mthd`, `ct_src_ltm`, `ct_srv_dst`, `is_sm_ips_ports`

I orchestrated a Spark ML Pipeline for our analysis, structured in the following stages:

- **Stages 1-2**: Transformation of each categorical column through StringIndexer and OneHotEncoder.
- **Stage 3**: Consolidation of all numerical columns and the output from OneHotEncoder into a unified feature vector via VectorAssembler.
- **Stage 4**: Implementation of a Random Forest Classifier as the concluding stage, tuned with specific hyperparameters.

### Random Forest Classifier Configuration
- **Number of Trees**: 150
- **Maximum Depth**: 15

The training phase involves fitting the model pipeline, which is subsequently preserved for future use.

During the testing phase, we reload the pipeline and apply it to the test dataset. This process yields predictions alongside valuable metrics for model evaluation.

### Evaluation Metrics
The model showcased an impressive accuracy rate of 97.286%, underscoring its efficacy in distinguishing between normal and malicious traffic within the dataset.


                 precision    recall  f1-score   support

           0         0.96     0.98        0.97        7376
           1         0.98     0.97        0.98        9097

    accuracy                           0.97      16473
    macro avg      0.97      0.97      0.97      16473
    weighted avg   0.97      0.97      0.97      16473
