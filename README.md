# 5G-intrusion-detection-dataset
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A public dataset of 5G core network traffic for intrusion detection research, generated with Open5GS and featuring multiple attack types.

This dataset was created as part of the research published in the papers listed below. We kindly ask that you cite our papers if you use this data for your own work.

## Table of Contents
- [Related Publications](#related-publications)
- [Dataset Description](#dataset-description)
- [Getting Started](#getting-started)
- [File Structure](#file-structure)
- [Data Dictionary](#data-dictionary)
- [How to Cite](#how-to-cite)
- [License](#license)
- [Contributing](#contributing)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

## Related Publications

The primary way to give credit for this dataset is by citing the associated peer-reviewed papers where it was used:

1.  **Sheikhi, S., & Kostakos, P. (2024).** *Safeguarding cyberspace: Enhancing malicious website detection with pso-optimized xgboost and firefly-based feature selection.* Computers & Security, 103885.
2.  **Sheikhi, S., & Kostakos, P. (2024).** *Advancing Security in 5G Core Networks through Unsupervised Federated Time Series Modeling.*
3.  **Sheikhi, S., & Kostakos, P. (2023).** *DDoS attack detection using unsupervised federated learning for 5G networks and beyond.* In 2023 Joint European Conference on Networks and Communications & 6G Summit (EuCNC/6G Summit) (pp. 442-447).

## Dataset Description

This dataset contains detailed packet-level features from a simulated 5G core network. The primary goal is to provide a rich source of data for developing and testing machine learning models for 5G security.

* **Network Environment:** Simulated using Open5GS and UERANSIM.
* **Key Scenarios Covered:**
    * Normal user traffic
    * **Simulated Anomalies:**
        * Distributed Denial of Service (DDoS) attacks (SYN Flood, UDP Flood)
        * Distributed Packet Forwarding Control Protocol (PFCP) attacks
        * Distributed IP Spoofing attacks

## Getting Started

To get started with the dataset, you can clone this repository and use a library like Pandas in Python to load and analyze the data.

**Prerequisites:**
* Python 3.8+
* Pandas, NumPy, Matplotlib

**Example Usage:**
```python
import pandas as pd
import numpy as np

# The training data is split into two subsets which can be combined.
try:
    # Load the training subsets
    df_train1 = pd.read_csv('data/Train_subset_1.csv')
    df_train2 = pd.read_csv('data/Train_subset_2.csv')
    
    # Combine them into a single training dataframe
    df_train = pd.concat([df_train1, df_train2], ignore_index=True)
    
    print("Training data loaded successfully!")
    print("Shape of the combined training dataset:", df_train.shape)
    
    # Load the test data
    df_test = pd.read_csv('data/Test_Data.csv')
    print("Shape of the test dataset:", df_test.shape)

except FileNotFoundError:
    print("Error: Dataset file not found. Please download the files first.")
    print("See the 'File Structure' section for instructions on data access.")
```

## File Structure

The data files are large and should be hosted on a service like Google Drive, Kaggle, or using Git LFS.

**Download Link:** [**INSERT YOUR DOWNLOAD LINK HERE**]

The data is provided in multiple CSV files:
* `Train_subset_1.csv` & `Train_subset_2.csv`: These contain training data and can be used separately or combined into a larger training set.
* `Test_Data.csv`: A unified test set containing all traffic types for evaluating the final model.

The repository should be structured as follows:
```
.
├── data/
│   ├── Test_Data.csv
│   ├── Train_subset_1.csv
│   └── Train_subset_2.csv
├── notebooks/
│   └── 1_basic_analysis.ipynb
├── .gitignore
├── LICENSE
└── README.md
```

## Data Dictionary

The dataset contains 45 features and 1 label column.

| # | Feature Name | Data Type | Description |
|---|---|---|---|
| 1 | `ip.len` | Float | Total length of the IP packet. |
| 2 | `ip.flags.df` | Float | "Don't Fragment" flag in the IP header. |
| 3 | `ip.flags.mf` | Float | "More Fragments" flag in the IP header. |
| 4 | `tcp.port` | Float | TCP source or destination port. |
| 5 | `tcp.window_size` | Float | TCP window size. |
| 6 | `tcp.ack_raw` | Float | Raw TCP acknowledgment number. |
| 7 | `ip.fragment` | Float | IP fragment offset. |
| 8 | `ip.fragment.count` | Float | Number of IP fragments. |
| 9 | `ip.fragments` | Float | Information about IP fragments. |
| 10 | `ip.ttl` | Float | Time-to-live value of the IP packet. |
| 11 | `ip.proto` | Float | Protocol number (e.g., 6 for TCP, 17 for UDP). |
| 12 | `tcp.window_size.1` | Float | Duplicate of TCP window size. |
| 13 | `tcp.ack` | Float | TCP acknowledgment number. |
| 14 | `tcp.seq` | Float | TCP sequence number. |
| 15 | `tcp.len` | Float | Length of the TCP segment. |
| 16 | `tcp.stream` | Float | TCP stream index. |
| 17 | `tcp.urgent_pointer`| Float | TCP urgent pointer field. |
| 18 | `tcp.flags` | Float | TCP flags (e.g., SYN, ACK, FIN). |
| 19 | `tcp.analysis.ack_rtt` | Float | Round-trip time for TCP acknowledgment. |
| 20 | `tcp.segments` | Float | Reassembled TCP segments. |
| 21 | `tcp.reassembled.length` | Float | Length of reassembled TCP data. |
| 22 | `http.request` | Float | Indicates if the packet is an HTTP request. |
| 23 | `udp.port` | Float | UDP source or destination port. |
| 24 | `udp.length` | Float | Length of the UDP datagram. |
| 25 | `frame.time_relative`| Float | Time since the first frame in the capture. |
| 26 | `frame.time_delta` | Float | Time since the previous frame. |
| 27 | `tcp.time_relative` | Float | Time relative to the start of the TCP stream. |
| 28 | `tcp.time_delta` | Float | Time delta for the TCP stream. |
| 29 | `gtp.ext_hdr` | Float | GTP extension header presence. |
| 30 | `gtp.ext_hdr.length` | Float | Length of the GTP extension header. |
| 31 | `gtp.ext_hdr.pdu_ses_con.pdu_type` | Float | PDU type in the GTP extension header. |
| 32 | `gtp.ext_hdr.pdu_ses_con.qos_flow_id` | Float | QoS Flow ID in the GTP extension header. |
| 33 | `gtp.ext_hdr.pdu_ses_cont.ppp` | Float | PPP bit in PDU session container. |
| 34 | `gtp.ext_hdr.pdu_ses_cont.rqi` | Float | RQI bit in PDU session container. |
| 35 | `gtp.flags` | Float | GTP flags. |
| 36 | `gtp.flags.e` | Float | GTP extension header flag. |
| 37 | `gtp.flags.payload` | Float | GTP payload type flag. |
| 38 | `gtp.flags.pn` | Float | GTP N-PDU number flag. |
| 39 | `gtp.flags.reserved`| Float | Reserved GTP flags. |
| 40 | `gtp.flags.s` | Float | GTP sequence number flag. |
| 41 | `gtp.flags.version` | Float | GTP protocol version. |
| 42 | `gtp.length` | Float | Length of the GTP packet. |
| 43 | `gtp.message` | Float | GTP message type. |
| 44 | `gtp.teid` | Float | GTP Tunnel Endpoint Identifier. |
| 45 | `label` | Integer | **0 for Normal, 1 for Anomaly/Attack.** |

## How to Cite

Please cite the relevant papers listed in the [Related Publications](#related-publications) section. For your convenience, here is a BibTeX entry for one of the primary papers:

```bibtex
@inproceedings{sheikhi2023ddos,
  title={DDoS attack detection using unsupervised federated learning for 5G networks and beyond},
  author={Sheikhi, Saeid and Kostakos, Panos},
  booktitle={2023 Joint European Conference on Networks and Communications \& 6G Summit (EuCNC/6G Summit)},
  pages={442--447},
  year={2023},
  organization={IEEE}
}
```

## License

This dataset is licensed under the **MIT License**. See the `LICENSE` file for more details.
