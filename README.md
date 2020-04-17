# Phx.Gen.Auth

An authentication system generator for Phoenix 1.5+ applications.

**_Note: This project is still a work in progress and is alpha quality at the moment._**

This project generates code from José Valim's [Auth PR][auth pr] and is up to date
through commit: [6637c8](https://github.com/dashbitco/mix_phx_gen_auth_demo/pull/1/commits/6637c85d30adb77f4f2f3088f7f9753d1827c99c).

## Overview

The purpose of `phx.gen.auth` is to generate a pre-built authentication system into
a Phoenix 1.5+ application that follows both security and elixir best practices. By generating
code into the user's application instead of using a library, the user has complete freedom
to modify the authentication system so it works best with their app. The following links
have more information regarding the motivation and design of the code this generates.

* José Valim's blog post - [An upcoming authentication solution for Phoenix](https://dashbit.co/blog/a-new-authentication-solution-for-phoenix)
* [Original pull request on bare phoenix app][auth pr]
* [Original design spec](https://github.com/dashbitco/mix_phx_gen_auth_demo/blob/auth/README.md)


## Usage

### Generating a Phoenix 1.5 app

`phx.gen.auth` must be installed into a Phoenix 1.5+ application.

*Until phoenix 1.5 is released, you'll need to clone [the phoenix repo](https://github.com/phoenixframework/phoenix)
and install the 1.5-dev installer with [these instructions](https://github.com/phoenixframework/phoenix/blob/master/installer/README.md).*

Once the installer is installed, a new project can be generated by running

    $ mix phx.new my_app

Please note, the `--no-ecto` and `--no-html` options are not supported.

### Installation

After running `mix phx.new`, `cd` into your application's directory (ex. `my_app`).

#### Basic installation

1. Add `phx_gen_auth` to your list of dependencies in `mix.exs`

    ```elixir
    def deps do
      [
        {:phx_gen_auth, github: "aaronrenner/phx_gen_auth", only: [:dev], runtime: false},
        ...
      ]
    end
    ```
1. Install and compile the dependencies

    ```
    $ mix do deps.get, deps.compile
    ```

#### Umbrella installation

1. `cd` into your project's web app directory (ex. `apps/my_app_web`)

    ```
    $ cd apps/my_app_web
    ```
1. Add `phx_gen_auth` to your list of dependencies in `mix.exs`

    ```elixir
    def deps do
      [
        {:phx_gen_auth, github: "aaronrenner/phx_gen_auth", only: [:dev], runtime: false},
        ...
      ]
    end
    ```
1. Install and compile the dependencies

    ```
    $ mix do deps.get, deps.compile
    ```

### Running the generator

From the root of your phoenix app (or `apps/my_app_web` in an umbrella app), you
can install the authentication system with the following command

    $ mix phx.gen.auth Accounts User users

This creates the templates,views, and controllers on the web namespace,
and a new `MyApp.Accounts` [context][phoenix contexts guide], in the application
namespace.

Next, let's install the dependencies and migrate the database

    $ mix deps.get
    $ mix ecto.migrate

Let's run the tests and make sure our new authentication system works as
expected.

    $ mix test

Finally, let's start the our phoenix server and try it out.

    $ mix phx.server

### Learning more

To learn more about `phx.gen.auth`, run the following command.

    $ mix help phx.gen.auth

You can also look up the mix task in hexdocs.

## License

Copyright 2020 Dashbit, Aaron Renner

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


[phoenix contexts guide]: https://hexdocs.pm/phoenix/contexts.html
[auth pr]: https://github.com/dashbitco/mix_phx_gen_auth_demo/pull/1
