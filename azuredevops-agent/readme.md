# Azure DEvops agent

<https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops>

## DEbug

```bash
docker run -e AZP_URL="https://dev.azure.com/REPLACEME" -e AZP_TOKEN="REPLACEME" -e AZP_POOL="k3s pool" dana23747/azure-devops-linux-agent:latest

docker build --tag dana23747/azure-devops-linux-agent:latest . && docker push dana23747/azure-devops-linux-agent:latest

'''