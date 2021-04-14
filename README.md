# Austin Flatiron API

This is a general API for creating objects to fetch in front end labs. 


## Faker 
Use the [Faker](https://github.com/faker-ruby/faker) gem to generate random names, locations, numbers, etc. to seed database.


## Add a Model
Add a model or models to the app: 
`rails g model name age:integer`

## Create PostgresQl db and migrate 
- `rails db:create`

- `rails db:migrate`

## Seed db
In seed.rb, create a new instace(s) of the model:

```
5.times {
    Model.create(
        name: Faker::Name.first_name,
        age: rand(18..99)
    )
}
```
Then run: 
- `rails db:seed`
- 
<em>DONT FORGET TO DESTROY MODELS FOR FUTURE RESEEDING.</em>
- `Model.destroy_all`

Start a console session and test data.
- `rails c`

## Add a Controller 
Add a controller and create an endpoint(s) to collect that data from:
- `rails g controller model index`

Then inside the index endpoint method:
```
def index
    models = Model.all
    render json: models 
end
```

## Add route(s)
In the config/routes.rb file: 
```
Rails.application.routes.draw do

  get '/models'

end
```

## Test endpoint
Start the rails server: 
- `rails s`

and open this in the browser: 
[http://localhost:3000/models](http://localhost:3000/)

You should see a json rendering of the seed data.

## Push To Heroku
- `git add .`
- `git commit -m 'push models to heroku'`
- `git push heroku master`
- `heroku run rake db:migrate`
- `heroku run rake db:seed`
