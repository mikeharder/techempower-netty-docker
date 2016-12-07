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
```
docker run -it --rm -p 8080:8080 techempower-netty
```
