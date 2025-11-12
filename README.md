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

docker exec -it deepwiki:ollama-local /bin/bash

docker rm deepwiki
sudo rm -rf ~/.adalflow

docker image ls
docker image rm deepwiki:ollama-local
docker build -f Dockerfile-ollama-local -t  deepwiki:ollama-local .

curl http://10.0.0.60:11434/api/tags


```


## REFERENCES
- https://github.com/AsyncFuncAI/deepwiki-open
- https://github.com/AsyncFuncAI/deepwiki-open/blob/main/Ollama-instruction.md
- docker interanl search:
- https://www.google.com/search?q=host.docker.internal+not+found&oq=host.docker.&gs_lcrp=EgZjaHJvbWUqDQgCEAAYkQIYgAQYigUyBggAEEUYOTINCAEQABiRAhiABBiKBTINCAIQABiRAhiABBiKBTINCAMQABiRAhiABBiKBTINCAQQABiRAhiABBiKBTIHCAUQABiABDIHCAYQABiABDIHCAcQABiABDIHCAgQABiABDIHCAkQABiABNIBCDUxNDFqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8
- temp fix for "No Valid XML""
- https://github.com/AsyncFuncAI/deepwiki-open/issues/390


