# Load testing stand

Stand for load testing with yandex tank and grafana dashboard

## Graph samples

Here is some sample graph.

![image](doc/assets/dashboard.png)

## Installing / Getting started

```bash
git clone https://github.com/l-SK-l/Yandex-Tank-influxDB-Grafana.git
cd Yandex-Tank-influxDB-Grafana
./start.sh
```
After start, the grafana board will open in the default browser with monitoring of load testing

## If something is wrong

### To create the Database
```bash
docker exec -it "CONTAINER ID" influx
> CREATE DATABASE influx
> SHOW DATABASES
> exit
```
### Permissions
If the database and dashboard do not load after start Docker
```bash
find . -type f -exec chmod +rx {} +
```
This command will recursively look through all files (-type f) in the current folder and its subfolders and then apply the chmod +rx command to all found files.

## Configuration

The project contains predefined settings in tests/config.yml

```yaml
phantom:
  enabled: true
  address: IP:PORT #Server address and port
  #ammofile: ammo.txt
  #ammo_type: uri
  uris: #Path
  - /index.html
  load_profile:
    load_type: rps
    schedule: line(10, 100, 60s)
  #load_profile:
    #load_type: instances
    #schedule: line(1,150,100s) const(150,2h)
  #headers:
   # - "[Host: www.example.com]"

# Uncomment this if you want to autostop load testing
# autostop:    
  # autostop: 
    # - http(5xx,25%,1s)  

console: #Console output at runtime
  enabled: true

telegraf:
  enabled: false

influx:
  enabled: true
  address: influx
  port: 8086
  database: influx
  tank_tag: 'mytank'
```
tests/ammo.txt contains settings of requests of load testing. You can write your ammo.txt generator and add it to start.sh script

If you want to know about a more advanced configuration of Yandex tank use the [link](https://yandextank.readthedocs.io/en/latest/config_reference.html)
