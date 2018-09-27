# **sg create**

Usage: jcloud sg create [OPTIONS] NAME
Creates some new security groups by the user
-f, --file Yaml file to create security group
--help Print usage

安全组yaml文件示例：

name: sg-test-1
description: sg-test-description
rules:
- direction: ingress
port_range_min: 22
port_range_max: 22
protocol: tcp
remote_ip_prefix: "0.0.0.0/0"