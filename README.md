# CloudScrape Ruby Client

Wrapper for CloudScrape API. 

* [API Documentation](https://app.cloudscrape.com/#/api)
* [Support](https://cloudscrape.zendesk.com/hc/en-us)

## Installation

Add this line to your application's Gemfile:

    gem 'cloud_scrape'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install cloud_scrape
    
## Configuration

``` ruby
CloudScrape.configure do |config|
  config.base_url = "https://app.cloudscrape.com/api/"
  config.api_key = "pol6BFzsASYw4gQBl02b24nt"
  config.account_id = "a814a8r2-a664-4rcb-759c-9de21744117a"
  config.user_agent = "MY-AGENT/1.0"
  config.timeout = 60000
  config.verbose = true
  config.log = true
  config.logger = Rails.logger
end
```
    
Some confirmation can be set by environment variables:

``` bash
CLOUND_SCRAPE_CLIENT_BASE_URL="https://app.cloudscrape.com/api/"
CLOUND_SCRAPE_CLIENT_API_KEY="pol6BFzsASYw4gQBl02b24nt"
CLOUND_SCRAPE_CLIENT_ACCOUNT_ID="a814a8r2-a664-4rcb-759c-9de21744117a"
CLOUND_SCRAPE_CLIENT_USER_AGENT="MY-AGENT/1.0"
CLOUND_SCRAPE_CLIENT_TIMEOUT=60000
CLOUND_SCRAPE_CLIENT_VERBOSE=true
CLOUND_SCRAPE_CLIENT_LOG=true
```

* `base_url` sets the CloudScrape API url `https://app.cloudscrape.com/api/`
* `api_key` sets the CloudScrape API Key `nil`
* `user_agent` sets the UserAgent sent to CloudScrape `CS-RUBY-CLIENT/1.0`
* `timeout` sets the CloudScrape API request timeout `3600`
* `verbose` should all output be printed to STDOUT `false`
* `log` should log message be printed `false`
* `logger` Logger object. `Logger`

## Basic Usage

``` ruby
# Execute execution for a run (optional arguments to override configuration)
client = CloudScrape.new(
  api_key: "pol6BFzsASYw4gQBl02b24nt",
  account_id: "a814a8r2-a664-4rcb-759c-9de21744117a",
  user_agent: "MY-AGENT/1.0"    
)

execution_id = client.runs.execute(run_id)

# Check execution state
client.executions.get(execution_id).running?
# => true

# Execution results
client.executions.result(execution_id)
# => { ... }

# Remove execution
client.executions.remove(execution_id)
```

## Testing

Ensure all environment variables are set before recording new VCR cassettes.

    # Includes Rubocop
    $ bin/rspec
    
## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/[my-github-username]/ParseHub/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
