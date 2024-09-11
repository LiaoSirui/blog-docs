## run-grafana-behind-a-proxy

- run-grafana-behind-a-proxy：<https://grafana.com/tutorials/run-grafana-behind-a-proxy/>

Grafana 配置 domain

```ini
[server]
domain = example.com
```

如果需要配置子路径

```ini
[server]
domain = example.com
root_url = %(protocol)s://%(domain)s:%(http_port)s/grafana/
serve_from_sub_path = true
```

## Oauth

```ini
role_attribute_path = "contains(name, 'adm') && 'Admin' || contains(roles[*], 'admin') && 'Admin' || contains(roles[*], 'editor') && 'Editor' || 'Viewer'"
```

其他配置

```ini
[auth.generic_oauth]
# ..
# prevents the sync of org roles from the Oauth provider
skip_org_role_sync = true

```

