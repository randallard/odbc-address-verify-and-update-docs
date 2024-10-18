---
layout: default
title: Welcome to Address Verify and Update Documentation
---

# Welcome to Address Verify and Update Documentation

## Navigation

{% for item in site.nav %}
- [{{ item.name }}]({{ site.baseurl }}{{ item.link }})
{% endfor %}

## Introduction

This application assists in collecting client addresses from the database, saving them to a csv file for processing with a service, such as PeachtreeData, then using the files returned by the service to update the database.

## Quick Start

- [Installation Guide]({{ site.baseurl }}{{ site.nav | where: "name", "Installation" | map: "link" | first }})
- [User Guide]({{ site.baseurl }}{{ site.nav | where: "name", "User Guide" | map: "link" | first }})
- [Development Guide]({{ site.baseurl }}{{ site.nav | where: "name", "Development Guide" | map: "link" | first }})


