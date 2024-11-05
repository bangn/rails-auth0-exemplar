# Steps to add Auth0 to a Rails App

## Prerequisites

- rails 7
- ruby 3.3.4

## Follow below steps

1. Add below to Gemfile

```ruby
gem "omniauth-auth0"
gem "omniauth-rails_csrf_protection"
```

Then run

```bash
bundle install
```

2. Copy controllers

```bash
cp -ra ./app/controllers/ path/to/your/new-rails-app/app
```

3. Copy views

```bash
cp -ra ./app/views/ path/to/your/new-rails-app/app
```

4. Update routes

Copy below to your `config/routes.rb`

```ruby
root "home#show"
get "/dashboard" => "dashboard#show"
get "/auth/auth0/callback" => "auth0#callback"
get "/auth/failure" => "auth0#failure"
get "/auth/logout" => "auth0#logout"
get "/auth/redirect" => "auth0#redirect"
```

5. Copy Auth0 config

```bash
cp ./config/initializers/auth0.rb path/to/your/new-rails-app/config/initializers/
cp ./config/auth0.yml path/to/your/new/new-rails-app/config/
cp ./config/application.rb path/to/your/new/new-rails-app/config/application.rb
```

6. Start database

If the postgres database container has not been started

```bash
docker-compose -f ./docker-compose.yml up -d
```

7. Create database

```bash
bundle exec rake db:create
```

8. Export necessary env

```bash
export AUTH0_DOMAIN=your_auth0_domain
export AUTH0_CLIENT_ID=your_auth0_client_id
export AUTH0_CLIENT_SECRET=your_auth0_client_secret
```

9. Start server

```bash
bundle exec rails s
```
