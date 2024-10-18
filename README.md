# BOSH Release for Python-Based HTTP Server

This repository contains a BOSH release for deploying and managing a simple Python-based HTTP server. 
The HTTP server is implemented using Python's built-in HTTP server module, which is available by default on most Linux distributions. 
This means you don't need any additional dependencies for Python or other libraries to run the server.

## Prerequisites

- **BOSH CLI**: Ensure you have BOSH CLI installed.
- **BOSH Director**: Ensure you have access to a BOSH environment with a director deployed.
- **Stemcell**: The deployment will use the `ubuntu-jammy` stemcell

## Steps to Create and Deploy the BOSH Release

### 1. Clone the Repository

First, clone the repository containing your BOSH release:

```bash
git clone https://github.com.nhairlahovic-evoila/http-server-bosh-release.git
cd http-server-bosh-release
```

### 2. Create the BOSH Release

Once the blob has been added and the repository is set up, create the BOSH release:
```bosh
bosh create-release --force
```

The `--force` flag is optional and it allows you to create the release even if there are uncommitted changes or if certain checks are not met. This will create a development release in the `dev_releases/spring-boot/` directory.

### 3. Upload the BOSH Release to the Director

Next, upload the newly created release to your BOSH director:
```bash
bosh upload-release
```

### 4. Upload the Stemcell

If you haven't uploaded the required stemcell (Ubuntu Jammy), do so now:
```bash
bosh upload-stemcell <path-to-ubuntu-jammy-stemcell>
```

### 5. Deploy Using the Manifest

Now, deploy HTTP server using your `manifest.yml`:
```bash
bosh -d http-server deploy manifest.yml
```

### 6. Access HTTP Server

Once the deployment is complete, the HTTP server will be running on the VM. The server will be listening on the configured port, which is defined in the manifest and set to `9090`.

You can access the app on the deployed VM's IP and port:
```bash
curl http://<vm-ip>:9090/
```

You can find the VM IP by running:
```bash
bosh -d http-server vms
```

### Notes

- You can modify the manifest to change the number of instances, VM type, or any other properties like `port`.
- To update or redeploy the application, modify the manifest as needed and run `bosh deploy` again.







