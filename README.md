# elk-with-filebeat-by-docker-compose
ELK with Filebeat by Docker-compose - Simple &amp; Easy way to file logging

## Work flow
- mylog -> filebeat -> logstash -> elasticsearch <- kibana

## Usage

### Make ELK with Filebeat
1. Docker & Docker-compose install (Ubuntu)
```
# Docker install
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $(whoami)
```
```
# Docker-compose install
sudo apt-get install docker-compose
```

2. Set to making your log file into 'mylog' folder.
- Filebeat can auto-detect to *.log file was made, updated and push it to logstash.

3. Docker-compose up command
```
docker-compose up -d
```

### Customize Config
- logstash.conf
```
# Change 'time.localtime' to your location time
filter {
  ...
  ruby {
    code => "event.set('indexDay', event.get('[@timestamp]').time.localtime('+09:00').strftime('%Y%m%d'))"
  }
}
```
