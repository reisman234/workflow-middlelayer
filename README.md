# Workflow Middle-Layer

This repository contains the documentation and images for the Middle-Layer components [Workflow-Api](https://github.com/reisman234/workflow-api) and [Workflow-Provisioner](https://github.com/reisman234/workflow-provisioner).

In combination with an [Eclipse Data Space Connector](https://github.com/eclipse-edc/Connector), both components allow an Compute Provider to offer his compute resources in form of WorkflowAssets. The WorkflowAsset describes of which resources the Workflow consist. At the moment a Workflow consist of a worker container, which is specified by a container image and the required hardware resources. Furthermore, the description lists the required input- and output-resources that the container needs or generates after its successful execution.


## Workflow-Provisioner

The [Workflow-Provisioner](https://github.com/reisman234/workflow-provisioner) implements an HttpProvisioner in the context of the Eclipse Dataspace Components. It is responsible for providing a workflow-api for a consumer (*ConsumerId*) which  requested a offered asset and registering the requested asset in the workflow-api, as well as managing the access information for the consumer to its deployed api. After the requested asset's contract expires, the release/deletion of all created resources in the cluster is triggered.

![workflow](./docs/middlelayer_workflow-provisioner.drawio.png)

## Workflow-Api

The [Workflow-Api](https://github.com/reisman234/workflow-api) implements a simple interface (*API*) for the consumer, which lists and controls the registered WorkflowAssets. The API communicates with various components, such as a workflow backend and a storage backend. Thus, the API has endpoints which, on the one hand, enable input resources to be uploaded to the storage backend and, analogously, result data to be downloaded. On the other hand, there are endpoints that control the workflow backend and thus enable the creation, scheduling and monitoring of workflow jobs.

A WorkflowJob is the execution of the job that defines the worker-image. After the worker-image has finished successfully, the generated result data is stored in the StorageBackend via the data-side-car component. From there, the data is accessible to the consumer via the API and can be loaded.

![workflow-api](./docs/middlelayer_workflow-api.drawio.png)

## Example Job

The example job [dummy-job](https://github.com/reisman234/dummy-job) was created for simple and quick testing purposes.