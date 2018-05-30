---
description: The Laravel Backend
---

# Laravel Backend

## Models

info

## Migrations

info

## Seeds

info

## GraphQL API

GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more.

Send a GraphQL query to your API and get exactly what you need, nothing more and nothing less. GraphQL queries always return predictable results. Apps using GraphQL are fast and stable because they control the data they get, not the server.

GraphQL queries access not just the properties of one resource but also smoothly follow references between them. While typical REST APIs require loading from multiple URLs, GraphQL APIs get all the data your app needs in a single request. Apps using GraphQL can be quick even on slow mobile network connections

### Rest API vs GraphQL API

* **Similar:** The list of endpoints in a REST API is similar to the list of fields on the `Query` and `Mutation` types in a GraphQL API. They are both the entry points into the data.
* **Similar:** Both have a way to differentiate if an API request is meant to read data or write it.
* **Different:** In GraphQL, you can traverse from the entry point to related data, following relationships defined in the schema, in a single request. In REST, you have to call multiple endpoints to fetch related resources.
* **Different:** In GraphQL, there’s no difference between the fields on the `Query` type and the fields on any other type, except that only the query type is accessible at the root of a query. For example, you can have arguments in any field in a query. In REST, there’s no first-class concept of a nested URL.
* **Different:** In REST, you specify a write by changing the HTTP verb from `GET` to something else like `POST`. In GraphQL, you change a keyword in the query.

![](../.gitbook/assets/image%20%282%29.png)

### GraphQL API in our project

you can find the code of the laravel backend with the graphql api on the master branch of [https://github.com/aythonhouttekier/smart-campus-laravel-backend](https://github.com/aythonhouttekier/smart-campus-laravel-backend)

#### Installation

Version 1.0 is released. If you are upgrading from older version, you can check [Upgrade to 1.0](https://github.com/Folkloreatelier/laravel-graphql/blob/develop/docs/upgrade.md).

#### **Dependencies:**

* Laravel 5.x
* GraphQL PHP

**1-** Require the package via Composer in your `composer.json`.

```text
{
  "require": {
    "folklore/graphql": "~1.0.0"
  }
}
```

**2-** Run Composer to install or update the new requirement.

```text
$ composer install
```

or

```text
$ composer update
```

#### Laravel &gt;= 5.5.x

**1-** Publish the configuration file

```text
$ php artisan vendor:publish --provider="Folklore\GraphQL\ServiceProvider"
```

**2-** Review the configuration file

```text
config/graphql.php
```

#### Laravel &lt;= 5.4.x

**1-** Add the service provider to your `config/app.php` file

```text
Folklore\GraphQL\ServiceProvider::class,
```

**2-** Add the facade to your `config/app.php` file

```text
'GraphQL' => Folklore\GraphQL\Support\Facades\GraphQL::class,
```

**3-** Publish the configuration file

```text
$ php artisan vendor:publish --provider="Folklore\GraphQL\ServiceProvider"
```

**4-** Review the configuration file

```text
config/graphql.php
```

you can define multiple schemas. Having multiple schemas can be useful if, for example, you want an endpoint that is public and another one that needs authentication.

You can define multiple schemas in the config/graphql.php:

```text
'schema' => 'default',

'schemas' => [
    'default' => [
        'query' => [
             'usersQuery' => UserQuery::class,
             'sensorsQuery' => SensorQuery::class,
             'measurementsQuery' => MeasurementsQuery::class,
             'locationsQuery' => LocationsQuery::class,
             'devicesQuery' => DevicesQuery::class,
        ],
        'mutation' => [
            //'updateUserEmail' => 'App\GraphQL\Query\UpdateUserEmailMutation'
        ]
    ],
]
```

#### Creating a query

In the graphQL api of our project we made a type and a query for all the models here I will give you the code from the query and type of the user model. You can find the code from the other models on github.

First we create a type.

`?php  
namespace App\GraphQL\Type;  
  
use GraphQL\Type\Definition\Type;  
use Folklore\GraphQL\Support\Type as BaseType;  
use GraphQL;  
use App\User;  
  
class UserType extends BaseType  
{   
  protected $attributes = [   
      'name' => 'UserType',   
      'description' => 'A UserType'   
];  
  
 public function fields()   
{   
    return [   
         'id' => [   
              'type' => Type::int()   
         ],  
         'name' => [   
              'type' => Type::string()   
         ],  
         'email' => [   
              'type' => Type::string()   
         ],   
         'password' => [   
              'type' => Type::string()   
         ],  
         'remember_token' => [ 'type' => Type::string()   
         ],  
    ];  
}}`

Add the type to the `config/graphql.php` configuration file

```text
'types' => [
    'User' => UserType::class, 
    'sensors' => SensorType::class, 
    'measurements' => MeasurementsType::class, 
    'locations' => LocationsType::class, 
    'devices' => DevicesType::class,
]
```

Then you need to define a query that returns this type \(or a list\). You can also specify arguments that you can use in the resolve method.

```text
namespace App\GraphQL\Query;

use App\User;
use GraphQL;
use GraphQL\Type\Definition\Type;
use GraphQL\Type\Definition\ResolveInfo;
use Folklore\GraphQL\Support\Query;

class UsersQuery extends Query
{
    protected $attributes = [
        'name' => 'users'
        'description' => 'a UserQuery'
    ];

    public function type()
    {
        return GraphQL::type('User');
    }

    public function args()
    {
        return [
          'id' => [ 
              'type' => Type::int() 
          ], 
          'name' => [ 
              'type' => Type::string() 
          ], 
          'email' => [ 
              'type' => Type::string() 
          ], 
          'password' => [ 
              'type' => Type::string() 
          ], 
          'remember_token' => [ 
              'type' => Type::string() 
          ],   
      ];
    }

    public function resolve($root, $args, $context, ResolveInfo $info)
    {
        if(isset($args['id'])) {
            return User::find($args['id']); 
        }
        else if(isset($args['name'])) { 
            return User::find($args['name']); 
        } 
        else if(isset($args['email'])) { 
            return User::find($args['email']); 
        }
        else if(isset($args['password'])) { 
            return User::find($args['password']); 
        }
        else if(isset($args['remember_token'])) { 
            return User::find($args['remember_token']); 
        }
        else {
            return User::all(); 
        }
    }
}
```

Add the query to the `config/graphql.php` configuration file

```text
'schemas' => [
    'default' => [
        'query' => [
            'users' => 'App\GraphQL\Query\UsersQuery'
            'sensorsQuery' => SensorQuery::class, 
            'measurementsQuery' => MeasurementsQuery::class, 
            'locationsQuery' => LocationsQuery::class, 
            'devicesQuery' => DevicesQuery::class,
        ],
        // ...
    ]
]
```

And that's it. First use the command  `php artisan serve`You should get a response that the laravel development server is running on 127.0.0.1:8000 then we should be able to query GraphQL with a request to the url `/graphiql.` Try a GET request with the following `query` input

```text
query UserStats {
  usersQuery (id: 1) {
    name
    email
    password
    remember_token
  }
}
```

The response from graphiql is then

```text
{
  "data": {
    "usersQuery": {
      "name": "Fernanda Costermans",
      "email": "fern.cos@telenet.be",
      "password": "jdfksjf",
      "remember_token": "tokenkjdfj"
    }
  }
}
```

We can also put some relationships in the graphQL API you can see the code for implementing relationships on my github.

Here is an example query after the implementation of relationships

```text
query LocationsStats {
  locationsQuery(id: 6) {
    id
    name
    roomnumber
    description
    devices {
      id
      name
      locations_id
      sensors {
        name 
        id
        measurement_unit
        measurements {
          id
          value
          sensor_id
        }
      }
      
    }
  }
}

```

The response then will be 

```
{
  "data": {
    "locationsQuery": {
      "id": 6,
      "name": "Embedded systems",
      "roomnumber": 2.65,
      "description": "Our hackerspace lab, sometimes there is some education also",
      "devices": [
        {
          "id": 6,
          "name": "dummy_device",
          "locations_id": 6,
          "sensors": [
            {
              "name": "Dummy_sensor",
              "id": 21,
              "measurement_unit": "Dummy_unit",
              "measurements": []
            },
            {
              "name": "temperature",
              "id": 22,
              "measurement_unit": "Celcius",
              "measurements": []
            },
            {
              "name": "humidity",
              "id": 23,
              "measurement_unit": "%",
              "measurements": []
            },
            {
              "name": "movement",
              "id": 24,
              "measurement_unit": "%",
              "measurements": [
                {
                  "id": 25,
                  "value": 20,
                  "sensor_id": 24
                },
                {
                  "id": 26,
                  "value": 21,
                  "sensor_id": 24
                },
                {
                  "id": 27,
                  "value": 22,
                  "sensor_id": 24
                },
                {
                  "id": 28,
                  "value": 23,
                  "sensor_id": 24
                },
                {
                  "id": 29,
                  "value": 24,
                  "sensor_id": 24
                },
                {
                  "id": 30,
                  "value": 25,
                  "sensor_id": 24
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

You can find the full code on my github under the master branch [https://github.com/aythonhouttekier/smart-campus-laravel-backend](https://github.com/aythonhouttekier/smart-campus-laravel-backend)



