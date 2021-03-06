# Gatekeeper
[![Language](https://img.shields.io/badge/Swift-3-brightgreen.svg)](http://swift.org)
[![Build Status](https://travis-ci.org/nodes-vapor/gatekeeper.svg?branch=master)](https://travis-ci.org/nodes-vapor/gatekeeper)
[![codecov](https://codecov.io/gh/nodes-vapor/gatekeeper/branch/master/graph/badge.svg)](https://codecov.io/gh/nodes-vapor/gatekeeper)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/nodes-vapor/gatekeeper/master/LICENSE)

Rate Limiter and SSL enforcing middleware.

## Integration
Update your `Package.swift` file.
```swift
.Package(url: "https://github.com/nodes-vapor/gatekeeper", majorVersion: 0)
```

## Getting started 🚀
Both the rate limiter and SSL-enforcing middleware are easy to configure and get running.

## SSLEnforcer 🔒
`SSLEnforcer` has three configurable fields: the error to be thrown, your `Droplet` and the environments you wish to enforce on. The environments defaults to `[.production]`.
```swift
let drop = Droplet()
// this will only enforce if running in `production` mode.
let enforcer = SSLEnforcer(error: Abort.notFound, drop: drop)
```

If you wish to secure your endpoints during development you can do the following:
```swift
let enforcer = SSLEnforcer(
    error: Abort.notFound,
    drop: drop,
    environments: [
        .production,
        .development
    ]
)
```

## RateLimiter ⏱
`RateLimiter` has two configurable fields: the maximum rate and the cache to use. If you don't supply your own cache the limiter will create its own, in-memory cache.

```swift
let limiter = RateLimiter(rate: Rate(10, per: .minute))
```

### The `Rate.Interval` enumeration
The currently implemented intervals are:
```swift
case .second
case .minute
case .hour
case .day
```

## Credits 🏆
This package is developed and maintained by the Vapor team at [Nodes](https://www.nodes.dk).

## License 📄
This package is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)