# OT-SOC Threat Intelligence Translator

**Bridging the Gap Between IT Security Operations and OT Infrastructure Protection**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Flask](https://img.shields.io/badge/Flask-3.0.0-green.svg)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📖 Overview

Security Operations Centers (SOCs) struggle to interpret alerts from Industrial Control Systems (ICS) and SCADA environments. Traditional IT security tools lack the operational context needed to assess risks in critical infrastructure. This project translates OT-specific network anomalies into SOC-readable threat intelligence, enabling faster incident response and better risk prioritization.

**Inspired by Professor Awais Rashid's research** at the University of Bristol on cyber security of connected critical infrastructure systems, this tool demonstrates practical implementation of academic concepts in automated threat detection and human-machine decision-making in security operations.

---

## 🎓 Academic Context & Research Inspiration

This project draws direct inspiration from Professor Awais Rashid's work at the Bristol Cyber Security Group, specifically:

### Key Research Papers That Informed This Project:

1. **Rashid, A., Gardiner, J., Green, B., & Craggs, B. (2020).** "Everything Is Awesome! or Is It? Cyber Security Risks in Critical Infrastructure." *CRITIS 2019, Lecture Notes in Computer Science*, vol 11777. Springer.
   - This paper discusses the complexities of managing cyber security risks in infrastructure shaped by competing stakeholder demands (managers, control engineers, IT personnel, field operators) - a core challenge this tool addresses by translating OT events into SOC language.

2. **Craggs, B., Rashid, A., Hankin, C., Antrobus, R., Șerban, O., & Thapen, N. (2019).** "A Reference Architecture for IIoT and Industrial Control Systems Testbeds." *2nd Conference on Living in the Internet of Things 2019*. IET.
   - Describes the need for research in non-live OT environments due to operational constraints - motivating the use of datasets for security analysis rather than live systems.

3. **Gardiner, J., Craggs, B., Green, B., & Rashid, A. (2019).** "Oops I Did it Again: Further Adventures in the Land of ICS Security Testbeds." *ACM Workshop on Cyber-Physical Systems Security & Privacy (CPS-SPC)*.
   - Discusses lessons learned from building ICS testbeds for security research, informing the design principles for analyzing industrial network traffic.

4. **Frey, S., Rashid, A., Anthonysamy, P., Pinto-Albuquerque, M., & Naqvi, S.A. (2019).** "The Good, the Bad and the Ugly: A Study of Security Decisions in a Cyber-Physical Systems Game." *IEEE Transactions on Software Engineering*, 45(5), 521-536.
   - Explores human decision-making in cyber-physical security contexts - directly informing this tool's focus on supporting SOC analyst decision-making rather than full automation.

### Core Research Themes Implemented:

From Professor Rashid's profile statement:
> *"This naturally ties in with my cyber security research which focuses on developing tools and techniques that are adaptable to the constantly changing threat patterns utilised by criminals online. I am particularly interested in security of cyber-physical systems, such as, industrial control systems and Internet of Things."*

This project embodies these themes by:
- **Adaptability**: Flexible alert rules allow customization for different industrial environments
- **Cyber-Physical Focus**: Risk scoring considers physical/safety impact, not just data confidentiality
- **Human-Machine Balance**: Dashboard designed to augment analyst capabilities, not replace them
- **Practical Security**: Tool focuses on operational deployment in real SOC workflows

### Academic Contributions

While this is an **engineering project** (not original research), it demonstrates:
- Practical implementation of academic security concepts
- Understanding of OT/IT convergence challenges identified in literature
- Application of standardized threat modeling (MITRE ATT&CK for ICS)
- Bridge between theoretical research and operational security tools

**Clear Distinction**: This tool applies existing research concepts to build a practical solution. It does not claim novel algorithms, new threat models, or empirical research findings. Credit for the underlying research insights belongs to Professor Rashid and collaborators at Bristol's Cyber Security Group.

---

## 🎯 Problem Statement

**The Challenge:**
As identified by Rashid et al. (2020), managing security in critical infrastructure is shaped by "competing demands of a variety of stakeholders" - SOC analysts receive ICS alerts but lack the operational context that control engineers possess. Key challenges include:

- IT security tools don't understand industrial protocols (Modbus, S7, DNP3)
- Risk scoring designed for IT environments doesn't translate to OT safety concerns
- SIEM systems need formatted data but OT tools export in incompatible formats
- Delayed incident response due to contextual gaps between IT and OT teams

**The Impact:**
- High false positive rates leading to alert fatigue
- Difficulty prioritizing threats based on operational vs. data impact
- Poor integration between OT monitoring and SOC workflows
- Potential for severe consequences in critical infrastructure

**This Solution:**
A practical tool that analyzes ICS network traffic, calculates OT-specific risk scores, maps threats to MITRE ATT&CK for ICS framework, and exports actionable intelligence to SIEM platforms - addressing the stakeholder communication gap identified in Rashid's research.

---

## ✨ Features

### Core Capabilities
- 📊 **Real-time ICS Traffic Analysis** - Processes network datasets from industrial environments
- 🎯 **OT-Specific Risk Scoring** - Calculates threats based on safety and operational impact (availability > integrity > confidentiality)
- 🗺️ **MITRE ATT&CK Mapping** - Correlates detected anomalies with ICS-specific attack techniques
- 📄 **Automated PDF Reports** - Generates SOC analyst-friendly incident reports with actionable guidance

### Advanced Features
- ⚙️ **Custom Alert Rules** - Define environment-specific detection rules for protocols and thresholds
- 🌐 **Threat Intelligence Integration** - Cross-reference detected IPs with threat databases (simulated)
- 📤 **Multi-Format SIEM Export** - Export alerts in CEF, JSON, Syslog, and CSV formats
- 📈 **Visual Risk Dashboard** - No-scroll interface displaying key metrics and attack patterns

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Frontend (HTML/CSS/JS)                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Dashboard  │  │    Modals    │  │   Exports    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└────────────────────────────┬────────────────────────────────┘
                             │ REST API
┌────────────────────────────▼────────────────────────────────┐
│                    Backend (Flask/Python)                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Analyzer   │  │ Risk Engine  │  │   Reports    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└────────────────────────────┬────────────────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  ICS Datasets   │
                    │  (CSV Format)   │
                    └─────────────────┘
```

### Technology Stack
- **Backend**: Python 3.8+, Flask, Pandas, NumPy, ReportLab
- **Frontend**: Vanilla JavaScript, CSS3, HTML5
- **Analysis**: scikit-learn for pattern detection
- **Standards**: MITRE ATT&CK for ICS, CEF, RFC 5424 (Syslog)

---

## 🚀 Quick Start

### Prerequisites
```bash
Python 3.8+
pip (Python package manager)
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/sdingo/ot-soc-analyzer.git
cd ot-soc-analyzer
```

2. **Install dependencies**
```bash
cd backend
pip install -r requirements.txt
```

3. **Download test dataset** (Choose one):

   **Option 1: WUSTL-IIOT-2018** (Recommended for beginners)
   - Link: https://www.cse.wustl.edu/~jain/iiot/index.html
   - Size: ~190 MB
   - Contains: Normal traffic + Reconnaissance attacks
   - Format: CSV with labeled features
   
   **Option 2: SWaT Dataset** (Advanced - Requires registration)
   - Link: https://itrust.sutd.edu.sg/itrust-labs_datasets/dataset_info/
   - Description: Secure Water Treatment testbed dataset
   - Contains: 11 days of data (7 days normal, 4 days with 36 attack scenarios)
   - Features: 51 sensors/actuators with network traffic
   - **Note**: Requires formal request and approval (1-2 days processing)
   - **Citation Required**: If used in publications, must cite Mathur & Tippenhauer (2016)
   
   Place downloaded CSV file in `datasets/` folder

4. **Start the backend server**
```bash
python app.py
```
Server runs on `http://localhost:5000`

5. **Start the frontend** (new terminal)
```bash
cd frontend
python -m http.server 8000
```
Open browser to `http://localhost:8000`

### Usage

1. **Upload Dataset**: Click "Upload ICS Dataset" and select your CSV file
2. **View Analysis**: Dashboard displays risk score, attack detection, and affected devices
3. **Custom Rules**: Define environment-specific detection rules
4. **Threat Intel**: Check detected IPs against threat databases (simulated)
5. **Export**: Generate PDF reports or export to SIEM formats (CEF, JSON, Syslog, CSV)
6. **Reset**: Clear analysis to process new dataset

---

## 📊 Dataset Support

### Tested Datasets
- **WUSTL-IIOT-2018** - SCADA network traffic with labeled reconnaissance attacks (93.93% normal, 6.07% attacks)
- **SWaT (Secure Water Treatment)** - Real water treatment testbed with 36 diverse attack scenarios
- **Custom ICS Datasets** - Any CSV with network features and attack labels

### Required CSV Format
```csv
timestamp,src_ip,dst_ip,protocol,dst_port,packet_size,label
1,192.168.1.10,192.168.1.100,modbus,502,120,Normal
2,192.168.1.50,192.168.1.100,s7,102,80,Attack
```

Columns can vary; analyzer adapts to available fields (protocol, port, packet size, labels).

---

## 🔬 Technical Implementation

### Risk Scoring Algorithm
Inspired by Rashid et al.'s (2020) discussion of stakeholder priorities in ICS environments:

```python
Risk Score = Base Attack Percentage × Protocol Criticality × Device Impact × Temporal Clustering
```

**Factors:**
- **Protocol-based weighting**: Modbus (502), S7 (102) higher risk than HTTP
- **Device criticality**: PLCs, RTUs prioritized over HMIs (following Purdue Model)
- **Attack clustering**: Rapid successive attacks increase score (reconnaissance indicator)
- **Packet anomalies**: Unusual sizes, non-standard ports flagged

**OT vs IT Priority Inversion:**
- IT Security: Confidentiality > Integrity > Availability
- OT Security: Availability > Integrity > Confidentiality
- This tool scores based on OT priorities (operational impact > data theft)

### MITRE ATT&CK for ICS Mapping
Automatically maps detected patterns to ICS-specific techniques:
- **T0842** - Network Sniffing (reconnaissance patterns)
- **T0836** - Modify Parameter (unauthorized writes to PLCs)
- **T0814** - Denial of Service (flooding attacks)

### SIEM Export Formats

**CEF (Common Event Format)** - For ArcSight, QRadar:
```
CEF:0|SyreOps|OT-SOC-Analyzer|1.0|ALERT-123|Attack Detected|3|rt=2025-11-06T12:00:00Z
```

**JSON** - For Splunk, ELK:
```json
{
  "timestamp": "2025-11-06T12:00:00Z",
  "source": "OT-SOC-Analyzer",
  "alerts": [...]
}
```

**Syslog (RFC 5424)** - Universal standard:
```
<3>1 2025-11-06T12:00:00Z ot-soc-analyzer - - - ALERT-123 Attack Detected
```

---

## 📸 Screenshots
 All screenshots included in zip folder
---

## 🎯 Use Cases

### 1. SOC Operations
- Rapid triage of ICS/SCADA alerts with operational context
- Risk assessment considering physical/safety implications
- Integration with existing SIEM workflows (CEF, JSON, Syslog export)

### 2. Incident Response
- Quick analysis of suspicious network traffic from ICS environments
- MITRE ATT&CK correlation for standardized threat intelligence
- Exportable evidence for post-incident reports and compliance

### 3. Security Research
- Baseline establishment for ICS environments using public datasets
- Attack pattern visualization across different industrial protocols
- Dataset analysis for threat modeling and security posture assessment

### 4. Training & Education
- Demonstrate OT/IT security differences (CIA vs AIC priority)
- Teach MITRE ATT&CK for ICS framework application
- Practice SOC analyst workflows without access to live systems

---

## 🚧 Limitations & Future Work

### Current Limitations
- **Simulated threat intelligence**: Not integrated with real APIs (AbuseIPDB, VirusTotal)
- **In-memory storage**: Custom rules not persisted between sessions
- **Single-file analysis**: No historical trend comparison across multiple datasets
- **CSV-only**: Does not support PCAP files or real-time network capture
- **No empirical validation**: Not tested against commercial ICS security products

### Planned Enhancements
- [ ] Real threat intel API integration (AbuseIPDB, VirusTotal, AlienVault OTX)
- [ ] Historical trend analysis with database storage (PostgreSQL)
- [ ] Machine learning for behavioral anomaly detection
- [ ] PCAP file support with Scapy integration
- [ ] Multi-dataset comparison dashboard (baseline vs incident)
- [ ] Automated response actions (SOAR integration)
- [ ] Docker containerization for easy deployment
- [ ] Cloud deployment options (AWS/Azure)
- [ ] Performance testing on larger datasets (>1GB)

---

## 🤝 Contributing

This is an educational project demonstrating practical application of research concepts. Contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📚 References & Resources

### Academic Research (Inspiration)
1. Rashid, A., Gardiner, J., Green, B., & Craggs, B. (2020). Everything Is Awesome! or Is It? Cyber Security Risks in Critical Infrastructure. *CRITIS 2019, LNCS*, vol 11777. Springer. https://doi.org/10.1007/978-3-030-37670-3_1

2. Craggs, B., Rashid, A., Hankin, C., et al. (2019). A Reference Architecture for IIoT and Industrial Control Systems Testbeds. *2nd Conference on Living in the Internet of Things 2019*. IET.

3. Gardiner, J., Craggs, B., Green, B., & Rashid, A. (2019). Oops I Did it Again: Further Adventures in the Land of ICS Security Testbeds. *ACM CPS-SPC Workshop*.

4. Frey, S., Rashid, A., Anthonysamy, P., et al. (2019). The Good, the Bad and the Ugly: A Study of Security Decisions in a Cyber-Physical Systems Game. *IEEE Trans. Software Eng.*, 45(5), 521-536.

### Datasets
- **WUSTL-IIOT-2018**: https://www.cse.wustl.edu/~jain/iiot/index.html
- **SWaT (Secure Water Treatment)**: https://itrust.sutd.edu.sg/itrust-labs_datasets/
  - Mathur, A. P., & Tippenhauer, N. O. (2016). SWaT: A Water Treatment Testbed for Research and Training on ICS Security. *CySWATER@CPSWeek 2016*, 31-36.

### Standards & Frameworks
- **MITRE ATT&CK for ICS**: https://attack.mitre.org/matrices/ics/
- **Common Event Format (CEF)**: ArcSight CEF Specification
- **RFC 5424**: The Syslog Protocol
- **NIST SP 800-82**: Guide to Industrial Control Systems (ICS) Security

### Related Organizations
- Bristol Cyber Security Group: https://www.bristol.ac.uk/engineering/research/csrc/
- RITICS (Research Institute on Trustworthy ICS): UK Research Program
- PETRAS (Cyber Security of IoT): National Centre of Excellence

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details

---

## 👤 Author

**Phiwokuhle Sdingo Kunene**
- GitHub: https://github.com/Sdingo
- LinkedIn: https://www.linkedin.com/in/phiwokuhlesdingo/
- Email: sdingokunene@gmail.com

---


**Built with 🛡️ for Critical Infrastructure Security**

*This project demonstrates practical application of academic security research in operational environments, bridging the gap between theoretical threat modeling and real-world SOC operations.*


**Disclaimer**: This is an educational engineering project demonstrating implementation of research concepts. It is not a commercial product, does not claim novelty in research methodology, and has not undergone formal security validation. Use in production environments requires thorough testing and validation.
