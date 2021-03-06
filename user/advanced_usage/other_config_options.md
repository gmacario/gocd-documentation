# Other config options

This is a list of some of the more advanced configuration options available.
These will typically need to be set before the start of the Go Server, unless
specified.

## How to set these options

### Environment variables

If an option specified below is of type "Environment Variable", then it needs to
be made available to the Go Server in a way that is specified by the operating
system (or distribution).

For instance, on Windows,
[here](https://msdn.microsoft.com/en-us/library/bb726962.aspx) is a page from
Microsft, explaining how to do this.

On Linux, you can use the /etc/default/go-server file, since it gets sourced by
the Go Server before it starts. A line like this:

``` export ENVIRONMENT_VAR_1="My variable" ```

will make that variable (```ENVIRONMENT_VAR_1```) available to the Go Server.

If you're using the ZIP package, and starting the Go Server manually, you can
use an appropriate mechanism to set the environment variable (could be a DOS
batch file, or a shell script).

### System properties

If an option specified below is of type "System property", then it will be a
Java system property, which needs to be provided to the Go Server, typically
prefixed with ```-D``` unless otherwise stated. So, if the property is called
```my.new.property``` and the value that needs to be set is ```true```, then the
Java system property to be used will be ```-Dmy.new.property=true```. Notice the
lack of a space between the ```-D``` and the property name.

On Windows, the procedure to set an extra system property is [detailed
here](../installation/install/server/windows.html#overriding-default-startup-arguments-and-environment).

On Linux and while using the ZIP package, extra system properties are specified
through the special environment variable, GO_SERVER_SYSTEM_PROPERTIES, which can
be set as specified in the ["Environment Variables"](#environment-variables)
section above.


## Options

<a name='cruise.listen.host'></a>
### cruise.listen.host - The host that the Go Server should bind to

- Name: cruise.listen.host
- Type: [System property](#system-properties)
- Restrictions: Should be a valid, bind-able IP address

The Go Server opens a listening socket, so that it can serve pages to users and
Go Agents. It needs to listen on a specific host. This host determines which
clients (users as well as Go Agents) can access the Go Server. By default, the
server listens on 0.0.0.0, which is the wildcard or "unspecified" address.
Usually, this means that the Go Server can be accessed through any network
interface. In some, more advanced networking setups, it might be needed to
override this, typically to 127.0.0.1, so that only clients local to the box can
access it.

Another way to set this, on Linux installations, is to set the [environment
variable](#environment-variables) SERVER_LISTEN_HOST, which is used by the
server startup shell script, to set the ```cruise.listen.host``` system property.


<a name='cruise.server.port'></a>
### cruise.server.port - HTTP port for the Go Server

- Name: cruise.server.port
- Type: [System property](#system-properties)
- Restrictions: Should be the number of a valid port that is not used by another
  process

Similar to the [cruise.listen.host](#cruise.listen.host) property, the value of
this property determines which port the Go Server binds to, and accepts HTTP
connections from. If not overridden, it is set to 8153.

See also: Sister property - [cruise.server.ssl.port](#cruise.server.ssl.port).


<a name='cruise.server.ssl.port'></a>
### cruise.server.ssl.port - HTTPS port for the Go Server

- Name: cruise.server.ssl.port
- Type: [System property](#system-properties)
- Restrictions: Should be the number of a valid port that is not used by another
  process

Similar to the [cruise.listen.host](#cruise.listen.host) property, the value of
this property determines which port the Go Server binds to, and accepts HTTPS
connections from. If not overridden, it is set to 8154.

See also: Sister property - [cruise.server.port](#cruise.server.port).


<a name='cruise.config.dir'></a>
### cruise.config.dir - Location of the configuration files

- Name: cruise.config.dir
- Type: [System property](#system-properties)
- Restrictions: Should be the directory, writeable by the Go Server process

Though not used often, this property can be used to change the location of the
Go Server's config directory. The default value of this property is specified
[here](../installation/installing_go_server.html#location-of-files-after-installation-of-go-server).

Changing this could have an impact on the ability to upgrade the Go Server, and
so, it's not recommended to change this.
