<div style="margin: 20px;">
  <img src="docs/images/nexlayer.png" alt="Nexlayer GitHub Banner">
</div>

# Kd-Chat Deepseek-r1

This repository is a fork of [KatieHarris2397/Kd-Chat-Deepseek-r1](https://github.com/KatieHarris2397/Kd-Chat-Deepseek-r1), enhanced with Nexlayer integration via a `nexlayer.yaml` configuration file.

## Table of Contents

1. [Demo Kd-Chat Deepseek-r1](#demo-kd-chat-deepseek-r1)
2. [The Kd-Chat `nexlayer.yaml` file](#the-kd-chat-nexlayeryaml-file)
3. [`nexlayer.yaml` Pod Configuration Schema](#nexlayeryaml-pod-configuration-schema)

## Demo Kd-Chat Deepseek-r1

Ready to see Kd-Chat in action? Follow these simple steps to demo the application:
1. **Fork this repository** to create a personal copy.
2. **Run the following cURL command** in the Kd-Chat directory. This will generate a URL to view your Kd-Chat application:
```bash
curl -X POST https://app.nexlayer.io/startUserDeployment -H "Content-type: text/x-yaml" --data-binary @nexlayer.yaml
```

**Launch Your Demo**: Once deployed, click on the provided URL to explore your Kd-Chat application live!

## The Kd-Chat `nexlayer.yaml` File

### Important Note on Images Used
The `nexlayer.yaml` file includes both the `katieharris/kd-chat` and `katieharris/ollama` images tagged with version `deepseek-r1` from DockerHub.  These images utilize Ollama's Deepseek-r1 1.5b model.

### Environment Variables
Shown below are the set environment variables for the `kd-chat` pod.  Some important notes on connecting to other pods:
- The `REACT_APP_API_URL` variable includes a connection string to the ollama pod in this deployment.  Here, it uses the Nexlayer `<pod-name>.pod` notation to set the hostname of the pod to connect to.  For example, `REACT_APP_API_URL` is set to `http://ollama.pod:11434` where `ollama` is the name given to the pod we want to connect to.  `ollama.pod` in turn provides the hostname at which we can reach the `ollama` pod at.

### `nexlayer.yaml`
```yaml
vars:
  REACT_APP_API_URL: http://ollama.pod:11434
  NODE_ENV: production
```

Want more information?  View the Nexlayer template documentation [here](https://github.com/Nexlayer/templates/blob/main/README.md).

## `nexlayer.yaml` Pod Configuration Schema
| Key | Definition | Why it matters | Examples |
|-----|------------|----------------|----------|
| **name** | A unique name to identify this service. | Each little machine (pod) must work correctly for your app to run—if one machine breaks, your whole app might not work and your friends wouldn't be able to use it. | `name: kd-chat` |
| **image** | Specifies the Docker container image (including repository info) to deploy for that pod. | This tells Nexlayer exactly which pre-built container to use for your live app. Choosing a solid image means your app runs in a proven, ready-to-go environment for all your users. | `image: "katieharris/kd-chat:deepseek-r1"` |
| **path** | For web-facing pods, defines the external URL route where users access the service. | This sets the web address path where users access your service. A well-defined path means your website, service or API is easily found, making your app look friendly and professional on Nexlayer Cloud. | `path: "/"` or `path: "/api"` |
| **servicePorts** | Defines the ports for external access or inter-service communication. | These ports are like the doorways that let users (or other services) connect to your app. Set them correctly, and your live app will be easily accessible and reliable on the web. | `servicePorts:`<br>`- 3000` |
| **vars** | Runtime environment variables defined as direct key-value pairs. Use `<pod-name>.pod` to reference other pods or `<% URL %>` for the deployment's base URL. | These are the settings that tell your live app how to connect to databases, APIs, and more. When they're set up right, your app adapts perfectly to the cloud environment, keeping your users happy. | `vars:`<br>`  REACT_APP_API_URL: http://ollama.pod:11434`<br>`  NODE_ENV: production`<br> |
| **volumes** | Optional persistent storage settings that ensure data isn't lost between restarts. Each volume includes a name, size, and a mountPath. | Volumes are like cloud hard drives for your app. They store important data (like database files) so that nothing is lost when your app updates or restarts, keeping your users' data safe. | `volumes:`<br>`- name: postgres-data`<br>`  size: 10Gi`<br>`  mountPath: /var/lib/postgresql` |
| **mountPath** | Within a volume configuration, specifies the internal file system location where the volume attaches. Must start with a "/". | This tells Nexlayer exactly where to plug in your volume within a running container. When set correctly, your live app can read and save data smoothly—ensuring a seamless user experience. | `mountPath: "/var/lib/postgresql"` |
