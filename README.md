# nsp

## About Node Security

Node Security helps you keep your node applications secure. With Node Security you can:

* Make use of the CLI tool to help identify known vulnerabilities in your own projects.
* Get access to Node Security news and information from the ^lift team.

## Installing the CLI (nsp)

* To install the Node Security command line tool: `npm install -g nsp`
* Then run `nsp --help` to find out more.

## Exceptions

The Node Security CLI supports adding exceptions. These are advisories that you have evaluated and personally deemed unimportant for your project.

In order to leverage this capability, create a `.nsprc` file in the root of your project with content like the following:

```js
{
  "exceptions": ["https://nodesecurity.io/advisories/12"]
}
```

The URLs used in the array should match the advisory link that the CLI reports. With this in place, you will no longer receive warnings about any advisories in the exceptions array.

Be careful using this feature. If you add code later that is impacted by an excluded advisory, Node Security has no way of knowing. Keep a careful eye on your exceptions.

## Proxy Support

The Node Security CLI has proxy support by using [proxy-agent](https://www.npmjs.com/package/proxy-agent).

The currently implemented protocol mappings are listed in the table below:


| Protocol   | Example
|:----------:|:--------:
| `http`     | `http://proxy-server-over-tcp.com:3128`
| `https`    | `https://proxy-server-over-tls.com:3129`
| `socks(v5)`| `socks://username:password@some-socks-proxy.com:9050` (username & password are optional)
| `socks5`   | `socks5://username:password@some-socks-proxy.com:9050` (username & password are optional)
| `socks4`   | `socks4://some-socks-proxy.com:9050`
| `pac`      | `pac+http://www.example.com/proxy.pac`



To configure the proxy set the proxy key in your `.nsprc` file. This can be put in the root of your project or in your home directory.

```js
{
    "proxy": "http://127.0.0.1:8080"
}
```



## Code Climate Node Security Engine

`codeclimate-nodesecurity` is a Code Climate engine that wraps the Node Security CLI. You can run it on your command line using the Code Climate CLI, or Code Climate's <a href="http://codeclimate.com">hosted analysis platform</a>.

Note that this engine *only* works if your code has a `npm-shrinkwrap.json` file committed.

### Testing

First, build this repo with docker

```
git clone git@github.com:nodesecurity/nsp
cd nsp
docker build -t codeclimate/codeclimate-nodesecurity .
```

Install the codeclimate CLI

```
brew tap codeclimate/formulae
brew install codeclimate
```

Go into your project's directory and enable codeclimate

```
codeclimate init
```

Then edit `.codeclimate.yml` to add the engine like so

```yaml
---
engines:
  nodesecurity:
    enabled: true
exclude_paths: []
```

And finally run it

```
codeclimate analyze --dev
```

## Contact

Node Security (+) is brought to you by [^lift security](https://liftsecurity.io).

## License

    Copyright (c) 2015 by ^Lift Security

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.

    See the License for the specific language governing permissions and
    limitations under the License.
