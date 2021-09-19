---
title: "Spinnaker Contributions"
date: 2021-09-19T13:16:36-07:00
draft: false
aliases: ["/posts/oss/spinnaker-contrib"]
showToc: true
summary: Contributions to the Spinnaker ecosystem while working at New Relic.
---

## Spin CLI `account` subcommand

Pull Request: [feat(cmd): add account sub command for querying configured accounts #324](https://github.com/spinnaker/spin/pull/234)

Added support for listing and getting accounts in Spinnaker.

## Halyard 

### Kubernetes custom resources

Pull Request: [feat(kubernetes): add flag for Kubernetes custom resources #1436](https://github.com/spinnaker/halyard/pull/1436)

Added support for adding and removing pre-configured Kubernetes custom resources associated with a specific Kubernetes cluster
account in Halyard/Spinnaker. This enabled display and some management of CRDs in Spinnaker by mapping a CRD to a Spinnaker kind.

### New Relic monitoring daemon

Pull Request: [feat(monitoring): add new relic monitoring daemon config #1442](https://github.com/spinnaker/halyard/pull/1442)

Added support for configuring New Relic monitoring daemon config.
