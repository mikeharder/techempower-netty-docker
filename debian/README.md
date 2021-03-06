# Build
## Common
```
git clone https://github.com/TechEmpower/FrameworkBenchmarks
```
## Host
```
sudo apt update
sudo apt install openjdk-8-jdk-headless
sudo apt install maven
cd FrameworkBenchmarks/frameworks/Java/netty
mvn clean compile assembly:single
```
## Container
```
cd FrameworkBenchmarks/frameworks/Java/netty
git submodule add https://github.com/mikeharder/techempower-netty-docker
docker build -t techempower-netty -f techempower-netty-docker/debian/Dockerfile .
```

# Run
## Host
```
cd FrameworkBenchmarks/frameworks/Java/netty
java -server -XX:+UseNUMA -XX:+UseParallelGC -XX:+AggressiveOpts -jar target/netty-example-0.1-jar-with-dependencies.jar
```
## Container
### Bridge Networking
```
docker run -it --rm -p 8080:8080 techempower-netty
```

### Host Networking
```
docker run -it --rm --network host techempower-netty
```

## Client
```
wget https://raw.githubusercontent.com/mikeharder/pipeline-lua/master/pipeline.lua
wrk -c 256 -t 32 -d 10 -s pipeline.lua http://server-ip-or-name:8080/plaintext -- 16
```
