---
tags:
  - azure-devops
  - npm
  - deployment
---

# Update SonicEquipmentUI npm publish token

The `azure-pipelines-1.yml` publish step uses a **service connection** named `SonicEquipmentUINPM` — the npm auth token lives there, not in the pipeline file itself.

## Steps

1. Go to the Azure DevOps project
2. **Project Settings** → **Service connections**
3. Find the connection named **`SonicEquipmentUINPM`**
4. Edit it and update the npm authentication token
