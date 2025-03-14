# @backstage/plugin-proxy-backend

## 0.2.29

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.15.0

## 0.2.29-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.15.0-next.0

## 0.2.28

### Patch Changes

- a4fa1ce090: The proxy-backend now automatically reloads configuration when app-config.yaml is updated.
- 72622d9143: Updated dependency `yaml` to `^2.0.0`.
- 8006d0f9bf: Updated dependency `msw` to `^0.44.0`.
- Updated dependencies
  - @backstage/backend-common@0.14.1

## 0.2.28-next.1

### Patch Changes

- a4fa1ce090: The proxy-backend now automatically reloads configuration when app-config.yaml is updated.
- 72622d9143: Updated dependency `yaml` to `^2.0.0`.
- Updated dependencies
  - @backstage/backend-common@0.14.1-next.3

## 0.2.28-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.14.1-next.0

## 0.2.27

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.14.0

## 0.2.27-next.1

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.14.0-next.2

## 0.2.27-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.6-next.0

## 0.2.26

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.3
  - @backstage/config@1.0.1

## 0.2.26-next.1

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.3-next.2
  - @backstage/config@1.0.1-next.0

## 0.2.26-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.3-next.0

## 0.2.25

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.2

## 0.2.25-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.2-next.0

## 0.2.24

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.1
  - @backstage/config@1.0.0

## 0.2.23

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.0

## 0.2.23-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.13.0-next.0

## 0.2.22

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.12.0

## 0.2.21

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.11.0

## 0.2.20

### Patch Changes

- Fix for the previous release with missing type declarations.
- Updated dependencies
  - @backstage/backend-common@0.10.9
  - @backstage/config@0.1.15

## 0.2.19

### Patch Changes

- c77c5c7eb6: Added `backstage.role` to `package.json`
- Updated dependencies
  - @backstage/backend-common@0.10.8
  - @backstage/config@0.1.14

## 0.2.18

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.7

## 0.2.18-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.7-next.0

## 0.2.17

### Patch Changes

- 332d3decb2: Adds a new option `skipInvalidTargets` for the proxy `createRouter` which allows the proxy backend to be started with an invalid proxy configuration. If configured, it will simply skip the failed proxy and mount the other valid proxies.

  To configure it to pass by failing proxies:

  ```
  const router = await createRouter({
    config,
    logger,
    discovery,
    skipInvalidProxies: true,
  });
  ```

  If you would like it to fail if a proxy is configured badly:

  ```
  const router = await createRouter({
    config,
    logger,
    discovery,
  });
  ```

- Updated dependencies
  - @backstage/backend-common@0.10.6

## 0.2.17-next.1

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.6-next.0

## 0.2.17-next.0

### Patch Changes

- 332d3decb2: Adds a new option `skipInvalidTargets` for the proxy `createRouter` which allows the proxy backend to be started with an invalid proxy configuration. If configured, it will simply skip the failed proxy and mount the other valid proxies.

  To configure it to pass by failing proxies:

  ```
  const router = await createRouter({
    config,
    logger,
    discovery,
    skipInvalidProxies: true,
  });
  ```

  If you would like it to fail if a proxy is configured badly:

  ```
  const router = await createRouter({
    config,
    logger,
    discovery,
  });
  ```

## 0.2.16

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.4
  - @backstage/config@0.1.13

## 0.2.16-next.0

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.4-next.0
  - @backstage/config@0.1.13-next.0

## 0.2.15

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.10.0

## 0.2.14

### Patch Changes

- bab752e2b3: Change default port of backend from 7000 to 7007.

  This is due to the AirPlay Receiver process occupying port 7000 and preventing local Backstage instances on MacOS to start.

  You can change the port back to 7000 or any other value by providing an `app-config.yaml` with the following values:

  ```
  backend:
    listen: 0.0.0.0:7123
    baseUrl: http://localhost:7123
  ```

  More information can be found here: https://backstage.io/docs/conf/writing

- Updated dependencies
  - @backstage/backend-common@0.9.11

## 0.2.13

### Patch Changes

- 957e4b3351: Updated dependencies
- Updated dependencies
  - @backstage/backend-common@0.9.6

## 0.2.12

### Patch Changes

- Updated dependencies
  - @backstage/backend-common@0.9.0
  - @backstage/config@0.1.8

## 0.2.11

### Patch Changes

- 13da7be3c: Clean up proxy creation log messages and make them include the mount path.

## 0.2.10

### Patch Changes

- 3108ff7bf: Make `yarn dev` respect the `PLUGIN_PORT` environment variable.
- 6ffcf9ed8: Bump http-proxy-middleware from 0.19.2 to 2.0.0
- Updated dependencies
  - @backstage/backend-common@0.8.3

## 0.2.9

### Patch Changes

- 875809a59: Fixed proxy requests to the base URL of routes without a trailing slash redirecting to the `target` with the full path appended.
- Updated dependencies [92963779b]
- Updated dependencies [eda9dbd5f]
  - @backstage/backend-common@0.8.2

## 0.2.8

### Patch Changes

- Updated dependencies [22fd8ce2a]
- Updated dependencies [f9fb4a205]
  - @backstage/backend-common@0.8.0

## 0.2.7

### Patch Changes

- cdb3426e5: Prefix proxy routes with `/` if not present in configuration
- Updated dependencies [e0bfd3d44]
- Updated dependencies [38ca05168]
- Updated dependencies [d8b81fd28]
  - @backstage/backend-common@0.7.0
  - @backstage/config@0.1.5

## 0.2.6

### Patch Changes

- Updated dependencies [8686eb38c]
- Updated dependencies [0434853a5]
- Updated dependencies [8686eb38c]
  - @backstage/backend-common@0.6.0
  - @backstage/config@0.1.4

## 0.2.5

### Patch Changes

- 1987c9341: Added a verification for well formed URLs when processing proxy targets. Otherwise users gets a cryptic error message thrown from Express which makes it hard to debug.
- 9ce68b677: Fix for proxy-backend plugin when global-agent is enabled
- Updated dependencies [497859088]
- Updated dependencies [8adb48df4]
  - @backstage/backend-common@0.5.5

## 0.2.4

### Patch Changes

- Updated dependencies [0b135e7e0]
- Updated dependencies [294a70cab]
- Updated dependencies [0ea032763]
- Updated dependencies [5345a1f98]
- Updated dependencies [09a370426]
  - @backstage/backend-common@0.5.0

## 0.2.3

### Patch Changes

- Updated dependencies [38e24db00]
- Updated dependencies [e3bd9fc2f]
- Updated dependencies [12bbd748c]
- Updated dependencies [e3bd9fc2f]
  - @backstage/backend-common@0.4.0
  - @backstage/config@0.1.2

## 0.2.2

### Patch Changes

- 6a6c7c14e: Filter the headers that are sent from the proxied-targed back to the frontend to not forwarded unwanted authentication or
  monitoring contexts from other origins (like `Set-Cookie` with e.g. a google analytics context). The implementation reuses
  the `allowedHeaders` configuration that now controls both directions `frontend->target` and `target->frontend`.
- 3619ea4c4: Add configuration schema for the commonly used properties
- Updated dependencies [612368274]
  - @backstage/backend-common@0.3.3

## 0.2.1

### Patch Changes

- Updated dependencies [1722cb53c]
- Updated dependencies [1722cb53c]
- Updated dependencies [7b37e6834]
- Updated dependencies [8e2effb53]
  - @backstage/backend-common@0.3.0

## 0.2.0

### Minor Changes

- 5249594c5: Add service discovery interface and implement for single host deployments

  Fixes #1847, #2596

  Went with an interface similar to the frontend DiscoveryApi, since it's dead simple but still provides a lot of flexibility in the implementation.

  Also ended up with two different methods, one for internal endpoint discovery and one for external. The two use-cases are explained a bit more in the docs, but basically it's service-to-service vs callback URLs.

  This did get me thinking about uniqueness and that we're heading towards a global namespace for backend plugin IDs. That's probably fine, but if we're happy with that we should leverage it a bit more to simplify the backend setup. For example we'd have each plugin provide its own ID and not manually mount on paths in the backend.

  Draft until we're happy with the implementation, then I can add more docs and changelog entry. Also didn't go on a thorough hunt for places where discovery can be used, but I don't think there are many since it's been pretty awkward to do service-to-service communication.

- 9226c2aaa: Limit the http headers that are forwarded from the request to a safe set of defaults.
  A user can configure additional headers that should be forwarded if the specific applications needs that.

  ```yaml
  proxy:
    '/my-api':
      target: 'https://my-api.com/get'
      allowedHeaders:
        # We need to forward the Authorization header that was provided by the caller
        - Authorization
  ```

### Patch Changes

- Updated dependencies [5249594c5]
- Updated dependencies [56e4eb589]
- Updated dependencies [e37c0a005]
- Updated dependencies [f00ca3cb8]
- Updated dependencies [6579769df]
- Updated dependencies [8c2b76e45]
- Updated dependencies [440a17b39]
- Updated dependencies [8afce088a]
- Updated dependencies [7bbeb049f]
  - @backstage/backend-common@0.2.0
