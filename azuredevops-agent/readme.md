# Azure DEvops agent

<https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops>

## DEbug

```bash
docker run -e AZP_URL="https://dev.azure.com/REPLACEME" -e AZP_TOKEN="REPLACEME" -e AZP_POOL="k3s pool" dana23747/azure-devops-linux-agent:latest

docker build --tag dana23747/azure-devops-linux-agent:latest . && docker push dana23747/azure-devops-linux-agent:latest

docker run -e AZP_URL="https://dev.azure.com/dana23746" -e AZP_TOKEN="h26htigstghqw3wdjibg7anlw6qz2mhfd4k66to66jsheftwu72a" -e AZP_POOL="k3s pool" dana23747/azure-devops-linux-agent:latest
'''