Celluloid::Redis
================

INCOMPLETE: sorry folks, this is still a work in progress

A Celluloid::IO-based connection backend for the [redis-rb][redisrb]
gem, providing "evented" connection support that can multiplex long-lived
blocking calls like pub/sub and blpop(rpush) with the Celluloid message
protocol.

[redisrb]: https://github.com/redis/redis-rb

## Why?

Is Celluloid going down the same path as EventMachine, requiring
Celluloid::IO-specific support for each library that touches the network?

Ideally, no! Celluloid::IO::TCPSocket is a duck type of Ruby's TCPSocket,
and where libraries provide a dependency injection API for the socket
class to use, it should be possible to use Celluloid::IO as a drop-in
replacement. An example of a library with an API like this is 'net/ssh',
which allows an `option[:proxy]` which (though oddly named) allows the
API user to dependency inject their own socket class.

The situation with redis-rb is a bit more... gnarly. Different socket
backends are provided for Ruby versus JRuby, for example, and no
dependency injection API is provided out-of-the-box.

The goal of `celluloid-redis` is to provide a stable Redis connection
backend which works across multiple Ruby platforms using a
Celluloid::IO-based socket backend.

Ideally this adapter can also leverage other Celluloid features to provide
nifty things like timeouts that actually work!

## Installation

Add this line to your application's Gemfile:

    gem 'celluloid-redis'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install celluloid-redis

## Usage

TODO: Write usage instructions here

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request