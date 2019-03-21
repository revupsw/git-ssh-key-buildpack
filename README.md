# git-ssh-key-buildpack

A Heroku buildpack for setting a private git SSH key as part of the application build. Particularly useful for granting Heroku access to installing a private git repository as a dependency.

# Configuration

1. Set up a deploy/access key with [GitHub](https://developer.github.com/v3/guides/managing-deploy-keys/).

2. Once you've generated the SSH key, configure the Heroku environment variable `GIT_DEPLOY_KEY`:

    ```shell
    $ heroku config:set GIT_DEPLOY_KEY="`cat /path/to/key`"
    ```

3. Add the buildpack to Heroku using either the CLI or the dashboard. It will need to run before any buildpack trying to get SSH access. In the following example, it runs before the `heroku/nodejs` buildpack:

    ```shell
    $ heroku buildpacks:set --index 1 https://github.com/poetic-labs/git-ssh-key-buildpack.git
    $ heroku buildpacks:add heroku/nodejs
    ```
