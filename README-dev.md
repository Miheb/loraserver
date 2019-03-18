# Start dev container (run once)
docker run -d -it --volume=$PWD:/go/src/github.com/brocaar/loraserver --name lora_server_dev khbx/lora_server_dev:latest

# Requirements (run once)
sudo docker exec lora_server_dev /bin/sh -c "make dev-requirements && make requirements"

# Compile and recreate imag
sudo docker exec lora_server_dev /bin/sh -c "make clean && make build" && sudo docker build -t theo024/loraserver -f Dockerfile-copy .

# Image was built using
docker build -f Dockerfile-devel -t khbx/lora_server_dev .
