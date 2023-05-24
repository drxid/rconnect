<p align="center">
  <a href="https://github.com/drxid/rconnect" target="_blank">
    <img src="https://i.ibb.co/bQggyJg/rcon.png" alt="rconnet" width="500">
  </a>
</p>

<p align="center">
  rconnect — is the RCON layer for Battlefield/Frostbite engine, powered by node.js and enhanced with Deno for modern code and type safety. <br>
  It enables easy creation of custom server management interfaces with automated map voting, team allocation, real-time player stats, and more.
<p>

## Usage

```ts
import { BF4Api, RconClient } from './src/mod.ts'

const ip = ''
const port = ''
const password = ''

async function main() {
  const rconClient = new RconClient(ip, port)
  try {
    const bf4 = new BF4Api(rconClient)
    await bf4.login(password)

    const serverInfo = await bf4.serverInfo()
    console.log('serverInfo', serverInfo)

    bf4.onPlayerKill$.subscribe((e) => console.log('onPlayerKill', e))
    await bf4.adminEvents('true')
  } catch (e) {
    console.error(e)
    rconClient.disconnect()
  }
}

main()
```

### For debug run your app
```
DEBUG=* deno run --allow-env --allow-net app.ts
```