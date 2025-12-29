# DeepWiki stuff

```
docker build -f Dockerfile-ollama-local -t  deepwiki:ollama-local .

docker run -p 3000:3000 -p 8001:8001 --name deepwiki \
  -v ~/.adalflow:/root/.adalflow \
  -e OLLAMA_HOST=your_ollama_host \
  deepwiki:ollama-local

docker run -p 3000:3000 -p 8001:8001 --name deepwiki \
  -v ~/.adalflow:/root/.adalflow \
  -e OLLAMA_HOST=10.0.0.60:11434 \
  deepwiki:ollama-local

docker run -it -p 3001:3000 -p 8001:8001 --name deepwiki  -v ~/.adalflow:/root/.adalflow  -e OLLAMA_HOST=http://10.0.0.60:11434 deepwiki:ollama-local /bin/bash

docker run -it -p 3001:3000 -p 8001:8001 --name deepwiki  -v ~/.adalflow:/root/.adalflow  -e OLLAMA_HOST=http://10.0.0.60:11434 -e OPENAI_API_KEY=na --add-host host.docker.internal:host-gateway deepwiki:ollama-local /bin/bash

docker run -it -p 3001:3000 -p 8001:8001 --name deepwiki -v ~/.adalflow:/root/.adalflow -e OLLAMA_HOST=http://10.0.0.60:11434 -e LLM_PROVIDER=ollama -e LLM_MODEL=qwen3:1.7b --add-host host.docker.internal:host-gateway deepwiki:ollama-local /bin/bash


docker run -it -p 3001:3000 -p 8001:8001 --name deepwiki -v ~/.adalflow:/root/.adalflow -e OLLAMA_HOST=http://10.0.0.60:11434 --add-host host.docker.internal:host-gateway deepwiki:ollama-local /bin/bash

docker run -it -p 3001:3000 -p 8001:8001 --name deepwiki -v ~/.adalflow:/root/.adalflow -e OLLAMA_HOST=http://10.0.0.60:11434 --add-host host.docker.internal:host-gateway deepwiki:ollama-local

docker exec -it deepwiki:ollama-local /bin/bash

docker rm deepwiki
sudo rm -rf ~/.adalflow

docker image ls
docker image rm deepwiki:ollama-local
docker build -f Dockerfile-ollama-local -t  deepwiki:ollama-local .

curl http://10.0.0.60:11434/api/tags


```

## Usage stuff for docker-compose.yml
```
# Start the container
docker-compose up -d

# Access the bash shell (equivalent to your -it flags)
docker-compose exec deepwiki /bin/bash

# View logs
docker-compose logs -f deepwiki

# Stop the container
docker-compose down
```

## Ollama increase model context

Inspect:

```
root@f4a230be2c38:/# ollama show nomic-embed-text:latest
  Model
    architecture        nomic-bert    
    parameters          137M          
    context length      2048          
    embedding length    768           
    quantization        F16           

  Capabilities
    embedding    

  Parameters
    num_ctx    8192    

  License
    Apache License               
    Version 2.0, January 2004    
    ...                          
```
Ollama context is 8192, but default model is 2048.

From: https://github.com/ollama/ollama/issues/6852

```
cat > Modelfile <<EOF
FROM llama3.1:8b
PARAMETER num_ctx 8192
EOF
$ ollama create llama3.1:8b-8kcontext

cat > Modelfile <<EOF
FROM nomic-embed-text:latest
PARAMETER num_ctx 8192
EOF
$ ollama create llama3.1:8b-8kcontext

cat > Modelfile <<EOF
FROM nomic-embed-text:v1.5
PARAMETER num_ctx 8192
EOF
$ ollama create nomic-embed-text:v1.5-8kcontext


```


## REFERENCES
- https://github.com/AsyncFuncAI/deepwiki-open
- https://github.com/AsyncFuncAI/deepwiki-open/blob/main/Ollama-instruction.md
- docker interanl search:
- https://www.google.com/search?q=host.docker.internal+not+found&oq=host.docker.&gs_lcrp=EgZjaHJvbWUqDQgCEAAYkQIYgAQYigUyBggAEEUYOTINCAEQABiRAhiABBiKBTINCAIQABiRAhiABBiKBTINCAMQABiRAhiABBiKBTINCAQQABiRAhiABBiKBTIHCAUQABiABDIHCAYQABiABDIHCAcQABiABDIHCAgQABiABDIHCAkQABiABNIBCDUxNDFqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8
- temp fix for "No Valid XML"
- https://github.com/AsyncFuncAI/deepwiki-open/issues/390
- possible fix for "Fetch Failed Error on using OLLAMA locally with nomic-embed-text and llama3.1:8b"
- https://github.com/ollama/ollama/issues/6852
- https://ollama.com/library/nomic-embed-text

- General for docker
- https://dev.to/mjnaderi/accessing-host-services-from-docker-containers-1a97
- get list of ports
- https://www.google.com/search?q=linux+list+ports+used&rlz=1C1GCEA_enUS1088US1088&oq=linux+list+ports+used&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQABiABDIICAIQABgWGB4yCAgDEAAYFhgeMggIBBAAGBYYHjIICAUQABgWGB4yCAgGEAAYFhgeMggIBxAAGBYYHjIICAgQABgWGB4yCAgJEAAYFhge0gEINDk5OGowajeoAgCwAgA&sourceid=chrome&ie=UTF-8
  - sudo ss -tulnp
  - sudo netstat -tulnp
  - sudo lsof -i -P -n | grep LISTEN

- for (future) compare
- https://github.com/mermaid-js/mermaid
- https://deepwiki.com/mermaid-js/mermaid
- different and cleaner than deepwiki-open