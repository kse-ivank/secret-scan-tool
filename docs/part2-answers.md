## Part 2 – Questions to Answer

**1. What is workflow_call and how is it different from workflow_dispatch?**  
workflow_call turns a workflow into a reusable component that other workflows can invoke and pass inputs to. Meanwhile workflow_dispatch is a manual trigger that lets a human start that specific workflow from the github ui

**2. Why does the job need packages: write permission?**  
Pushing images to GHCR y is implemented as publishing packages, so the job needs packages: write to allow the docker actions and build-push-action to authenticate with GITHUB_TOKEN and actually push images

**3. Why does the workflow only log in to the registry when push is true?**  
Logging in is only necessary when an image will be pushed to the remote registry, so skipping the login step when push is false avoids unnecessary use of credentials.

**4. What is the benefit of GHA cache (cache-from/cache-to: type=gha)?**  
The github actions cache stores Docker build layers between workflow runs so that unchanged layers can be reused instead of rebuilt from scratch, which speeds up repeated builds

**5. Why is python:3.12-slim used instead of the full image?**  
The -slim variant contains the same python runtime but without optional tools and libraries, making the image much smaller and faster to pull and start

**6. What is the difference between ENTRYPOINT and CMD here?**  
ENTRYPOINT defines the base command that will always run when the container starts, while CMD supplies the default arguments that are passed to that entrypoint

**7. How does volume mounting (-v) allow scanning files outside the container?**  
With docker run -v /host/path:/scan, Docker mounts a host directory into the container’s filesystem, making the host files visible inside the container under scan, it allows scanning host files without copying them to the image

