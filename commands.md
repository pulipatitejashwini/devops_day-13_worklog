# Commands Used

## 1. Prometheus Installation
`cd /tmp`                
`wget https://github.com/prometheus/prometheus/releases/download/v2.45.6/prometheus-2.45.6.linux-amd64.tar.gz`                      
`tar -xvf prometheus-2.45.6.linux-amd64.tar.gz`                
`cd prometheus-2.45.6.linux-amd64`                   

`sudo mkdir -p /usr/local/bin/prometheus`                  
`sudo cp -rf * /usr/local/bin/prometheus`                             

## 2. Prometheus Service
`sudo vi /etc/systemd/system/prometheus.service`             

[Unit]             
Description=Prometheus Service             
After=network.target               

[Service]            
Type=simple             
ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml                  
WorkingDirectory=/usr/local/bin/prometheus                 

[Install]                    
WantedBy=multi-user.target                   

`sudo systemctl daemon-reload`                    
`sudo systemctl start prometheus`                   
`sudo systemctl enable prometheus`                    

## 3. Node Exporter
`wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz`                  
`tar -xvf node_exporter-1.8.1.linux-amd64.tar.gz`                   
`cd node_exporter-1.8.1.linux-amd64`                    

`sudo mkdir -p /usr/local/bin/node-exporter`               
`sudo cp -rf * /usr/local/bin/node-exporter`                      

`sudo vi /etc/systemd/system/node-exporter.service`                        

[Unit]               
Description=Prometheus Node Exporter                 
After=network.target             

[Service]               
Type=simple                  
ExecStart=/usr/local/bin/node-exporter/node_exporter                   

[Install]              
WantedBy=multi-user.target                 

`sudo systemctl daemon-reload`                  
`sudo systemctl start node-exporter`                  
`sudo systemctl enable node-exporter`                      

## 4. Prometheus Scrape Config
Edit prometheus.yml
`vi prometheus.yml`                 
scrape_configs:                    
  - job_name: "prometheus"                   
    static_configs:                    
      - targets: ["localhost:9090"]                

  - job_name: "node_exporter"                
    static_configs:                
      - targets: ["localhost:9100"]                     

`sudo systemctl restart prometheus`                    

## 5. Grafana Installation
`sudo apt update`                    
`sudo apt install grafana-enterprise -y`                    
`sudo systemctl start grafana-server`                        
`sudo systemctl enable grafana-server`                       

## 6. PromQL Queries
CPU Load:               
node_load1                      

Free RAM (MB):                
node_memory_MemFree_bytes /1024/1024                  

Disk Free (GB):            
node_filesystem_avail_bytes /1024/1024/1024                   

Memory Used %:                 
(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes)                  
/ node_memory_MemTotal_bytes * 100                     

## 7. Load Simulation
`sudo apt install stress-ng -y`                 
CPU + RAM + Disk load:                   
`stress-ng --cpu 2 --vm 1 --vm-bytes 2G --hdd 1 --timeout 900s`                    
