# Configuring & Startup

## Configuring the LexFloatServer

LexFloatServer uses a simple YAML-based text file as its config file. It expects a `config.yml` file to be in the same directory as LexFloatServer. If the config file is in some other directory it can be passed using the **"-c"** option.

The config is loaded at the start of the server. Any changes to the config file will be ignored until the server is restarted.

## Starting LexFloatServer in terminal

For testing purposes, you can easily run the LexFloatServer in the terminal (command prompt). To start the server simply pass the **"-s"** option:

```bash
lexfloatserver -s
```

{% hint style="info" %}
You need admin rights to run the LexFloatServer.&#x20;
{% endhint %}
