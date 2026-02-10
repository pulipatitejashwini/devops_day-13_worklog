# Monitoring Basics Using Prometheus & Grafana

## Overview
This project demonstrates system observability using **Prometheus, Node Exporter and Grafana**.                             
System metrics such as CPU, Memory and Disk were collected from a Linux server and visualized in Grafana dashboards. Load was simulated using stress-ng to observe real-time changes.                          

---

## Architecture
User → Grafana (3000)             
Grafana → Prometheus (9090)                 
Prometheus → Node Exporter (9100)              

---

## VM Configuration
### Prometheus Server
- OS: Ubuntu 22.04       
- CPU: 2 vCPU       
- RAM: 4 GB          
- Disk: 20 GB           
- Ports: 22, 9090, 9100          

### Grafana Server
- OS: Ubuntu 22.04          
- CPU: 2 vCPU               
- RAM: 4 GB             
- Disk: 20 GB          
- Ports: 22, 3000                 

## Tools Used
- Prometheus – Metric collection               
- Node Exporter – System metrics                 
- Grafana – Visualization                
- stress-ng – Load simulation                

## Metrics Collected

| Component | PromQL Query |
|---------|--------------|
| CPU Load | `node_load1` |
| Free RAM | `node_memory_MemFree_bytes` |
| Disk Free | `node_filesystem_avail_bytes` |
| Memory Used % | `(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100` |

## Dashboard Panels
1. **CPU Load (1 min)**               
2. **Free RAM (MB)**                    
3. **Available Disk (GB)**               

Dashboard Name: **System Monitoring Dashboard**             
## Load Testing           
System load was generated using:                
- CPU Load  
- RAM  
- Disk I/O

Graphs in Grafana showed clear spikes proving real-time monitoring.          

## Outcome
- Understood Prometheus scraping mechanism  
- Learned PromQL queries  
- Visualized metrics using Grafana  
- Observed system behavior under load

## Deliverables
- Grafana dashboard screenshot  
- Prometheus targets page  
- Exported dashboard JSON  
- This documentation

## Conclusion
This task helped in understanding **system observability**, monitoring architecture and real-time performance analysis using Prometheus and Grafana.
