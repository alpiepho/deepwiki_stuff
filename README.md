# DeepWiki stuff

```
docker run -p 3000:3000 -p 8001:8001 --name deepwiki \
  -v ~/.adalflow:/root/.adalflow \
  -e OLLAMA_HOST=your_ollama_host \
  deepwiki:ollama-local

docker run -p 3000:3000 -p 8001:8001 --name deepwiki \
  -v ~/.adalflow:/root/.adalflow \
  -e OLLAMA_HOST=10.0.0.60:11434 \
  deepwiki:ollama-local
```


## REFERENCES
- https://github.com/AsyncFuncAI/deepwiki-open
- https://github.com/AsyncFuncAI/deepwiki-open/blob/main/Ollama-instruction.md


