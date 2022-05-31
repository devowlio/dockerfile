# Dockerfile

Common `Dockerfile`'s for [devowl.io](https://devowl.io) projects.

- `/wp-react-starter/gitlab-ci`: Base image for [WP React Starter](https://github.com/devowlio/wp-react-starter/)'s [`gitlab-ci`](https://github.com/devowlio/wp-react-starter/tree/master/devops/docker/gitlab-ci).
- `/wordpress`: WordPress image with additional tools extending from the official WordPress image

# Build and Push

In order to push it to the registry (), you need to run the following commands:

```
docker build . --tag "devowliode/wp-react-starter-gitlab-ci:latest"
docker push devowliode/wp-react-starter-gitlab-ci:latest
```
