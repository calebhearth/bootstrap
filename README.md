# Bootstrapping: Making your app newbie-proof

Companies have lots of applications with lots of different setups. There should
be a QUICK AND EASY way to step into an unfamiliar app.

## Enter script/bootstrap

Put a file called `bootstrap` in the `script/` directory. The purpose of this
file will be to allow anyone to easily jump into a project and start
contributing.

script/bootstrap takes care of:
* dependency checks
* bundler
* db creation
* db migration
* db seeding
* static page compilation
* language compilation

### dependency checks

Is your database engine installed? (here's how to install it)
Is some_required_application running? (here's how to run it)

### bundler

```
bundle install \
  --binstubs \
  --local \
  --path=vendor/gems \
  --without=production
```

### db creation

`rake db:create`

### db migration

`rake db:migrate`

### db seeding

* pull database from production app
* `rake db:seed`
* `script/replicate-repo`

### static page compilation

404, 500

### language compilation

python, c, erlang...

## But running script/bootstrap takes forever...

**cache bootstrap results**

```
md5      << File.read('Gemfile')
checksum  = md5.hexdigest
installed = File.read('.bundle/checksum').strip
```

Running `script/bootstrap` should be fast, straightforward, and require no
knowledge of the underlying language or app setup.

## What else can I use script/bootstrap for?

You can also run script/bootstrap during any process that loads the environment,
like `script/server`.

You can even use `script/bootstrap` in your testing environment.

Add `script/cibuild` to your projects. This will allow you to keep test config
in the repository.

Your CI server only needs to ever run `script/cibuild`.

### cibuild? What's this noise?

```
export RACK_ROOT=["..."]
export RACK_ENV=["test"]

script/bootstrap

bin/rake
```

BOOM!

