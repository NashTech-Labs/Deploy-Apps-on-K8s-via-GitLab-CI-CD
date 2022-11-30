This techhub template basically help you to automatically deploy *new apps* in kubernetes cluster using gitlab ci-cd .
When a new application is created by a developer, the pipeline fails at the stage where it tries to update the Kubernetes deployment because the deployment files for new application doesn't exist . But using this pipeline you just need to update the variables of template file and you are ready to go for new applications.
After this Yaml template file is created, we need to make it accessible to the pipeline, there are some requirements for that:
- There is one pipeline for all applications.
- The yaml template file should be stored in a central place.
- The yaml template file should not be modified by any application or pipeline run.

#### Use this kubectl command to create a Kubernetes configmap from the yaml template file:

```kubectl -n <namespace-name> create configmap template-app --from-file=template=template.yaml```

#### This command puts the contents of the template.yaml file into a configmap. To access the contents from your Kubernetes cluster.

```kubectl -n <namespace-name> get configmap template-app -o jsonpath='{.data.template}'```
