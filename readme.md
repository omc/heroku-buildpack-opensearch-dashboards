# Heroku Buildpack for OpenSearch Dashboards

This buildpack downloads and installs OpenSearch Dashboard into a Heroku app slug.

## Compatibility

Tested versions: 1.0.0 and 1.2.2

## Usage

To use as a standalone buildpack:

```sh
    # Create a new project with the --buildpack option.
    mkdir opensearch-dashboards1 && cd opensearch-dashboards1 && git init
    heroku create opensearch-dashboards1 --buildpack https://github.com/omc/heroku-buildpack-opensearch-dashboards

    # Let OpenSearch Dashboards know where to find OpenSearch.
    heroku config:set OPENSEARCH_URL="https://osd_user:osd_pass@host.region.bonsaisearch.net"

    # Create a Procfile to run the OpenSearch Dashboard web server.
    echo 'web: opensearch-dashboards --port $PORT' > Procfile

    # Push the above to trigger a deploy.
    git add . && git commit -am "OpenSearch Dashboards setup" && git push heroku master

    # Open the app in your browser. You may be prompted for a username/password, which
    # matches the username and password of your OpenSearch URL.
    heroku open
```

### Private Spaces + VPC Peering

If you are using VPC peering from a private space, the automatic version detection will not work since the compile phase is run outside of the private space.

You must set the addition config vars.

```sh
    # Set the verison.
    heroku config:set OPENSEARCH_VERSION="1.2.2"
```
