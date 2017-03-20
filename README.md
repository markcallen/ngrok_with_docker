# ngrok_with_docker
Using ngrok with docker to create public URLs for your local development environment

## Setup

Create the www container
````
docker container run -v $(pwd)/public:/usr/share/nginx/html -p 80 -p 443 --name www -d nginx
````

Start the tunnel
````
docker run -d -p 4040 --link www:http --name www_ngrok wernight/ngrok ngrok http www:80
````

## Usage

Open the NGROK API

````
open http://$(docker port www_ngrok 4040)
````

Get the public https url - use the public_url value

````
curl $(docker port www_ngrok 4040)/api/tunnels/command_line | python -mjson.tool
````
