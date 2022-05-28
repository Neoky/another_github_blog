---
title: "Opensearch"
date: 2021-12-06T18:56:55-06:00
draft: true
---

# Opensearch

I use managed Elastic Opensearch and self-managed Opensearch in Kubernetes. I will try and keep everything here.

## Modify Opensearch and add plugins
Example Dockerfile
```docker
FROM opensearch:latest

RUN bin/opensearch-plugin install repository-s3
```

# References

* Opensearch plugins
https://opensearch.org/docs/latest/opensearch/install/plugins/