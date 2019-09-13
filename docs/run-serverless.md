# run-serverless

Runs complete serverless instance in preconfigured environment, limited to predefined plugins and hook events.

Optionally serverless instance can be freshly required with specifc modules mocked

## Usage

```javascript
const runServerless = require('@serverless/test/run-serverless');

describe('Some suite', () => {
  it('Some test that involves creation of serverless instance', function() {
    runServerless(pathToServerlessRootFolder, {
      // Options, see below documentation
    }).then(serverless => {
      // Resolved after serverless.run() finalizes.
      // Examine here expected outcome
    });
  });
});
```

### Supported options

#### `cwd`

Working directory in which supposedly `serverless` is run

#### `cliArgs` (optional)

CLI arguments (e.g. `['deploy', '--stage', 'beta']`), defaults to `[]`

#### `env` (optinal)

Eventual environment variables (e.g. `{ SLS_DEBUG: '*' }`)

#### `pluginPathsWhiteList`

Paths to plugins of which registered hooks should be invoked.  
Note: All other plugins will be naturally initialized but no hooks they registered will be invoked

#### `hookNamesWhiteList`

List of hooks for which callbacks should be run.
Registered callbacks for all other scheduled hooks will be ignored

#### `modulesCacheStup` (optional)

When provided, serverless instance will be created out of freshly required module,
and provided cache map will be used as stub for underlying required modules.