# Home Assistant Add-on: CouchDB

![Supports aarch64 Architecture][aarch64-shield] ![Supports amd64 Architecture][amd64-shield] ![Supports armv7 Architecture][armv7-shield]

CouchDB is a database that uses JSON for documents, JavaScript for MapReduce indexes, and regular HTTP for its API.

## About

This add-on provides a CouchDB database server for Home Assistant. CouchDB is a NoSQL database that stores data as JSON documents and provides a RESTful HTTP API for interacting with the database.

## Installation

1. Add this repository to your Home Assistant Supervisor
2. Install the "CouchDB" add-on
3. Configure the add-on (see configuration section below)
4. Start the add-on
5. Check the logs to see if everything went well

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
port: 5984
username: "admin"
password: "your_secure_password_here"
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `port`

The port number CouchDB will listen on. Default is 5984.

### Option: `username`

The admin username for CouchDB.

### Option: `password`

The admin password for CouchDB. **This is required and must be set!**

## Accessing CouchDB

Once the add-on is running, you can access the CouchDB web interface:

- Local: `http://homeassistant.local:5984/_utils/`
- IP: `http://YOUR_HA_IP:5984/_utils/`

Use the configured username and password to log in.

## Data Persistence

The add-on automatically stores CouchDB data in the Home Assistant configuration directory under `/config/couchdb/`. This ensures your databases persist across add-on restarts and updates.

## Support

Got questions?

You have several options to get them answered:

- The [Home Assistant Community Add-ons Discord chat server][discord] for add-on
  support and feature requests.
- The [Home Assistant Discord chat server][discord-ha] for general Home
  Assistant discussions and questions.
- The Home Assistant [Community Forum][forum].
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

You could also [open an issue here][issue] GitHub.

## Contributing

This is an active open-source project. We are always open to people who want to
use the code or contribute to it.

We have set up a separate document containing our
[contribution guidelines](CONTRIBUTING.md).

Thank you for being involved! :heart_eyes:

## Authors & contributors

The original setup of this repository is by [Your Name][your-name].

For a full list of all authors and contributors,
check [the contributor's page][contributors].

## License

MIT License

Copyright (c) 2025 Your Name

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[contributors]: https://github.com/db1996/hassio-addons/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/repository-community-hass-io-add-ons/24705?u=frenck
[your-name]: https://github.com/db1996
[issue]: https://github.com/db1996/hassio-addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/db1996/hassio-addons